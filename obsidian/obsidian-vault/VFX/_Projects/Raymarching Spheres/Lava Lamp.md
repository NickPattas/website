# Dynamic Metaballs with PBR Lighting in Unreal Engine 5.3

  

> A comprehensive guide to building a scalable, raymarched metaballs system with advanced physically-based rendering

  

---

  

## 📋 Project Overview

  

**Goal**: Create a lava lamp-style metaballs effect in Unreal Engine using HLSL raymarching with:

- Dynamic sphere system (easily add/remove spheres without code changes)

- Advanced PBR lighting (fresnel, metallic, roughness, environment reflections)

- Smooth blending between metaballs using smooth minimum function

  

**Implementation**: Custom HLSL shader in Unreal Engine 5.3 Material Editor

**Technique**: Raymarching with signed distance fields (SDF)

**Language**: HLSL (High-Level Shader Language)

  

---

  

## 🎯 The Challenge

  

### Original Problem

The initial metaballs implementation required manually duplicating ~30 lines of code for each new sphere:

- Distance calculation with noise displacement

- Smooth minimum blending

- Normal calculation

- Lighting calculations (diffuse + specular)

  

This was tedious, error-prone, and not scalable.

  

### Solution Architecture

Refactored to a **dynamic array-based system** where:

1. All spheres stored in arrays (`sphereCenters[]`, `sphereRadii[]`)

2. Loops handle distance calculations and blending

3. Single parameter (`NumberofSpheres`) controls active sphere count

4. Integrated custom PBR lighting model for realistic rendering

  

---

  

## 📊 System Architecture

  

```

Input Parameters → Raymarch Loop → SDF Evaluation → Lighting → Output

                      ↓

                 Sphere Arrays

                      ↓

              Smooth Minimum Blend

                      ↓

                Surface Detection

                      ↓

           Multi-Sphere PBR Lighting

```

  

### Key Components

  

1. **Raymarching Engine**: Steps through 3D space along view rays

2. **Signed Distance Field**: Calculates distance to metaball surface

3. **Smooth Minimum**: Blends multiple spheres organically

4. **PBR Lighting System**: Realistic material rendering

  

---

  

## 💻 Code Evolution

  

### Stage 1: Original Metaballs (Manual Duplication)

  

```hlsl

// Original code - required manual duplication for each sphere

float3 rayOrigin = 1 - (viewDir - worldPos);

float3 rayStep = viewDir * (-1);

  

float3 lightDirection = normalize(lightPos);

  

for(int i=0; i<st; i++) {

    float3 displace01 = sphereCenter01 + noisescale  * (sin(rayOrigin.x * time) +

        sin(rayOrigin.y * time) +

        sin(rayOrigin.z * time));

  

    float3 displace02 = sphereCenter02 + noisescale  * (sin(rayOrigin.x * time) +

        sin(rayOrigin.y * time) +

        sin(rayOrigin.z * time));

  

    float3 d1 = length(rayOrigin - displace01) - sphereRadius01;

    float3 d2 = length(rayOrigin - displace02) - sphereRadius02;

  

    float h = clamp(0.5 + 0.5 * (d2 - d1)/k, 0.0, 1.0);

  

    float d = lerp(d2, d1, h) - k*h*(1.0-h);

  

    if(d < 0.01) {

        float3 normal01 = normalize(rayOrigin - displace01);

        float3 normal02 = normalize(rayOrigin - displace02);

  

        float diffuse01 = max(dot(normal01, lightDirection), 0);

        float diffuse02 = max(dot(normal02, lightDirection), 0);

  

        float3 reflection01 = reflect(lightDirection, normal01);

        float3 reflection02 = reflect(lightDirection, normal02);

  

        float3 viewDirection = normalize(-worldPos - rayOrigin);

  

        float specular01 = pow(max(dot(reflection01, viewDirection), 0), 16);

        float specular02 = pow(max(dot(reflection02, viewDirection), 0), 16);

  

        float specular = specular01 + specular02;

        float diffuse = diffuse01 + diffuse02;

  

        outMask = 1;

        return diffuse + specular;

    }

  

    rayOrigin += rayStep;

}

  

outMask = 0;

return 0.;

```

  

**Problems:**

- ❌ Each new sphere requires ~30 lines of duplicated code

- ❌ Error-prone copy-paste process

- ❌ Hard to maintain and modify

- ❌ Basic lighting model only

  

---

  

### Stage 2: Custom PBR Lighting Model

  

```hlsl

// Custom lighting shader with PBR features

float3 rayOrigin = 1 - (viewDir - worldPos);

float3 rayStep = viewDir * (-1);

  

float3 lightDirection = normalize(lightPos);

  

for(int i=0; i<st; i++) {

    float d = length(rayOrigin - sphereCenter) - sphereRadius;

  

    if(d < 0.01) {

        float3 normal = normalize(rayOrigin - sphereCenter);

  

        // Fresnel effect

        float3 fresnel = lerp(saturate(pow(saturate(1-dot(normal, viewDir)), 5) + 0.04),

                             baseColor, metallic);

  

        // Lambert Diffuse

        float3 diffuse = saturate(dot(normal, lightDirection));

  

        // Ambient Diffuse (hemisphere lighting)

        float3 ambientLight = lerp(lerp(groundColor, midColor, saturate(normal.z + 1)),

                                  skyColor, saturate(normal.z));

  

        float3 reflection = reflect(lightDirection, normal);

        float3 viewDirection = normalize(-worldPos - rayOrigin);

  

        // Ambient Reflections (environment mapping)

        float3 envreflections = TextureCubeSampleLevel(texObject, texObjectSampler,

                                                      reflect(viewDirection, normal),

                                                      lerp(0, 8, roughness)) * fresnel;

  

        // Phong Specular

        float3 specular = pow(saturate(dot(reflection, viewDirection)),

                             exp((1 - roughness) * 10 + 1)) * diffuse * fresnel;

  

        outMask = 1;

  

        return ((specular + (diffuse * lerp(baseColor, 0, metallic))) * lightColor) +

               (ambientLight * lerp(baseColor, 0, roughness)) +

               envreflections;

    }

  

    rayOrigin += rayStep;

}

  

outMask = 0;

return 0.;

```

  

**Key Features:**

- ✅ **Fresnel Effect**: Rim lighting based on view angle

- ✅ **Metallic Parameter**: Controls metal vs. dielectric appearance

- ✅ **Roughness Parameter**: Surface finish from mirror to matte

- ✅ **Hemisphere Lighting**: Sky/ground ambient colors

- ✅ **Environment Reflections**: Cubemap sampling with blur

- ✅ **Advanced Specular**: Roughness-driven highlights

  

---

  

### Stage 3: Final Implementation (Dynamic + PBR)

  

```hlsl

// Combined Dynamic Metaballs with Custom PBR Lighting

#define MAX_SPHERES 8

  

float3 rayOrigin = 1 - (viewDir - worldPos);

float3 rayStep = viewDir * (-1);

float3 lightDirection = normalize(lightPos);

  

float3 sphereCenters[MAX_SPHERES];

float sphereRadii[MAX_SPHERES];

  

sphereCenters[0] = sphereCenter01;

sphereCenters[1] = sphereCenter02;

sphereCenters[2] = sphereCenter03;

  

sphereRadii[0] = sphereRadius01;

sphereRadii[1] = sphereRadius02;

sphereRadii[2] = sphereRadius03;

  

// Number of active spheres

int numSpheres = int(NumberofSpheres);

  

for(int i = 0; i < st; i++) {

    // Calculate displaced positions for all spheres

    float3 displacedPositions[MAX_SPHERES];

    float distances[MAX_SPHERES];

  

    for(int s = 0; s < numSpheres; s++) {

        displacedPositions[s] = sphereCenters[s];

        distances[s] = length(rayOrigin - displacedPositions[s]) - sphereRadii[s];

    }

  

    // Smooth minimum operation for all spheres

    float d = distances[0];

    for(int s = 1; s < numSpheres; s++) {

        float h = clamp(0.5 + 0.5 * (d - distances[s]) / k, 0.0, 1.0);

        d = lerp(d, distances[s], h) - k * h * (1.0 - h);

    }

  

    // Check if we hit the metaball surface

    if(d < 0.01) {

        // Calculate lighting contribution from all spheres

        float3 totalLighting = float3(0, 0, 0);

  

        for(int s = 0; s < numSpheres; s++) {

            float3 normal = normalize(rayOrigin - displacedPositions[s]);

  

            // Fresnel effect

            float3 fresnel = lerp(saturate(pow(saturate(1 - dot(normal, viewDir)), 5) + 0.04),

                                 baseColor, metallic);

  

            // Lambert Diffuse

            float3 diffuse = saturate(dot(normal, lightDirection));

  

            // Ambient Diffuse (hemisphere lighting)

            float3 ambientLight = lerp(lerp(groundColor, midColor, saturate(normal.z + 1)),

                                      skyColor, saturate(normal.z));

  

            // Reflection vector

            float3 reflection = reflect(lightDirection, normal);

            float3 viewDirection = normalize(-worldPos - rayOrigin);

  

            // Ambient Reflections (environment mapping)

            float3 envreflections = TextureCubeSampleLevel(texObject, texObjectSampler,

                                                          reflect(viewDirection, normal),

                                                          lerp(0, 8, roughness)) * fresnel;

  

            // Phong Specular

            float3 specular = pow(saturate(dot(reflection, viewDirection)),

                                 exp((1 - roughness) * 10 + 1)) * diffuse * fresnel;

  

            // Combine all lighting components for this sphere

            float3 sphereLighting = ((specular + (diffuse * lerp(baseColor, 0, metallic))) * lightColor) +

                                   (ambientLight * lerp(baseColor, 0, roughness)) +

                                   envreflections;

  

            totalLighting += sphereLighting;

        }

  

        // Average the lighting contributions from all spheres

        totalLighting /= (float)numSpheres;

  

        outMask = 1;

        return totalLighting;

    }

  

    rayOrigin += rayStep;

}

  

outMask = 0;

return 0;

```

  

**Improvements:**

- ✅ Dynamic sphere management via arrays

- ✅ Single parameter to control sphere count

- ✅ Full PBR lighting per sphere

- ✅ Averaged lighting contributions

- ✅ Scalable to MAX_SPHERES (default: 8)

- ✅ No code changes needed to add/remove spheres

  

---

  

## 🔧 Technical Deep Dive

  

### Raymarching Algorithm

  

**Concept**: Step along view ray until surface intersection detected

  

```

1. Initialize ray origin and direction

2. For each step (0 to st):

   a. Calculate distance to nearest surface

   b. If distance < threshold: HIT → calculate lighting

   c. Else: advance ray by step size

3. If no hit: return background

```

  

**Parameters:**

- `st`: Raymarch steps (32-128) - quality vs. performance trade-off

- `rayStep`: Direction and magnitude of each step

- Threshold: `0.01` - surface detection sensitivity

  

---

  

### Signed Distance Field (SDF)

  

**Sphere SDF:**

```hlsl

float sphereSDF(float3 point, float3 center, float radius) {

    return length(point - center) - radius;

}

```

  

**Properties:**

- Negative = inside sphere

- Zero = on surface

- Positive = outside sphere

- Magnitude = distance to surface

  

---

  

### Smooth Minimum Function

  

**Purpose**: Blend multiple SDFs organically

  

```hlsl

float smoothMin(float d1, float d2, float k) {

    float h = clamp(0.5 + 0.5 * (d2 - d1) / k, 0.0, 1.0);

    return lerp(d2, d1, h) - k * h * (1.0 - h);

}

```

  

**Parameters:**

- `d1, d2`: Distance values to blend

- `k`: Blend factor (10-50)

  - Lower k = sharper transition

  - Higher k = smoother, more "blobby" blend

  

**Visual Effect:**

```

k = 10:  Sharp necking between spheres

k = 25:  Smooth, natural blend

k = 40:  Very organic, flowing transition

```

  

---

  

### PBR Lighting Components

  

#### 1. Fresnel Effect

```hlsl

float3 fresnel = lerp(

    saturate(pow(saturate(1 - dot(normal, viewDir)), 5) + 0.04),

    baseColor,

    metallic

);

```

- Schlick's approximation

- Creates bright edges at grazing angles

- Modulated by metallic parameter

  

#### 2. Lambert Diffuse

```hlsl

float3 diffuse = saturate(dot(normal, lightDirection));

```

- Simple cosine law

- Diffuse intensity = cos(angle between normal and light)

  

#### 3. Hemisphere Ambient Lighting

```hlsl

float3 ambientLight = lerp(

    lerp(groundColor, midColor, saturate(normal.z + 1)),

    skyColor,

    saturate(normal.z)

);

```

- Normals pointing up → skyColor

- Normals horizontal → midColor

- Normals pointing down → groundColor

- Creates realistic ambient gradient

  

#### 4. Environment Reflections

```hlsl

float3 envreflections = TextureCubeSampleLevel(

    texObject,

    texObjectSampler,

    reflect(viewDirection, normal),

    lerp(0, 8, roughness)

) * fresnel;

```

- Samples environment cubemap

- Mip level controlled by roughness (blur)

- Modulated by fresnel for realistic metal/dielectric behavior

  

#### 5. Phong Specular

```hlsl

float3 specular = pow(

    saturate(dot(reflection, viewDirection)),

    exp((1 - roughness) * 10 + 1)

) * diffuse * fresnel;

```

- Specular exponent from roughness

- Lower roughness = sharper highlights

- Energy-conserving (multiplied by diffuse)

  

#### Combined Lighting

```hlsl

float3 result =

    ((specular + (diffuse * lerp(baseColor, 0, metallic))) * lightColor) +

    (ambientLight * lerp(baseColor, 0, roughness)) +

    envreflections;

```

  
  

#UnrealEngine #HLSL #Raymarching #PBR #Metaballs #ShaderProgramming #GameDev #TechnicalArt