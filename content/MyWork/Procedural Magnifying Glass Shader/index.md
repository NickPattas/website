---
title: "Procedural Magnifying Glass Shader - Personal Project"
showReadingTime: false
showDate: false
showWordCount: false
orderBy: "weight"
weight: 3
---

Softwares used:
* Unreal Engine 5.7
* Houdini

{{< youtube g3TGO4nfVJ0 >}}

The idea was to create a procedural shader that allows me to art direct the physical properties of a lens like distortions, magnification and reflections.

{{< youtube NO09Zi1JY8c >}}

The magnifying glass was modeled and textured procedurally in Houdini using the Copernicus system of Houdini 21.0, making it easy to create iterations fast and with full control.

{{< youtube E4V9exKrGJ4 >}}

The main goal was for the shader to be lightweight, efficient and easy to use.

The scene color was sampled using Niagara's GBuffer Interface and stored in a Render Target Texture to then be sampled in the material.

This technique allows the user to have maximum control over the size and resolution of the texture.

![](assets/img/niagara.png)

![](assets/img/grid_init.png)

![](assets/img/grid_res.png)

![](assets/img/rt_write.png)

The dynamic focus, magnification and distortions of the lens were driven by a Line Trace logic inside the Blueprint Actor of the asset.

The distance between a surface and the focal point of the lens drives every other parameter of the shader.

![](assets/img/line_trace_01.png)

![](assets/img/line.png)

![](assets/img/trace_channel.png)

![](assets/img/collisions.png)

![](assets/img/remap.png)

![](assets/img/resolution.png)

Every important parameter is stored in a Material Parameter Collection to be easily accessible through Blueprints, Niagara Systems and Material Shaders.

![](assets/img/mpc_float.png)

![](assets/img/mpc_vector.png)

The shader was developed with efficiency and art-directability in mind.

![](assets/img/material_overview.png)

The actual lens of the model is just a 2D plane that, with the use of a spherical normal texture, creates the illusion of a thick magnifying lens.

![](assets/img/normals.png)

The normal texture was used to create complex spherical distortions and to resize the Scene Color texture. Additionally, a blur amount value based on the Mipmap levels creates the illusion of defocusing when the lens is far away from a surface.

![](assets/img/distortions.png)

All lighting properties like reflections, shadows and highlights were calculated with textures and simple masks to keep the effect as optimized as possible.

![](assets/img/reflections.png)

![](assets/img/light_calculations.png)

A custom shadow parameter was added using the "Shadow Pass Switch" node to further increase the realism of the effect.

![](assets/img/shadow.png)

Read the complete breakdown for the Modeling:
{{< button href="https://nickpattas.com/posts/magnifying-glass-part-1/" target="_blank" >}}
Modeling breadown
{{< /button >}}

Read the complete breakdown for the Shader:
{{< button href="https://nickpattas.com/posts/magnifying-glass-part-2/" target="_blank" >}}
Shader breakdwon
{{< /button >}}