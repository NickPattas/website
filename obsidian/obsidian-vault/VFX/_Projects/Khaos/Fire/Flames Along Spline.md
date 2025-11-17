Resources:
https://www.overdraw.xyz/
https://www.youtube.com/watch?v=Lz_DKV3irL4

![[Drawing 2025-10-06 13.00.17.excalidraw|1000]]

The **FIRST** and **LAST** Particle's Position along the Spline can be sampled using the Position Attribute Reader. 
In case of using a Ribbon is possible to use those Positions to overwrite the Ribbon's Facing.

![[Pasted image 20251007125141.png]]

Custom Decal Material.

![[Pasted image 20251010122415.png]]

***This way is possible to use decal shaders with GPU Niagara Particles.***

![[Pasted image 20251010122519.png]]

***Using sine waves in World Position Offset can add a lot of detail on the flames.***


## GEOMETRY

### BLENDER IMPLEMENTATION

It's possible to create a **Flames_Geometry Tool** with **Geometry Nodes in Blender**.

![[Pasted image 20251010123307.png]]
The displacement of the Curve is based on a simple **Sine Function.**
![[Pasted image 20251010123332.png]]
Using a float Curve adjusting the shape of the geometry along the curve.
![[Pasted image 20251010123500.png]]

![[Pasted image 20251010122908.png]]

After bake the **Geometry Nodes** into a **Static Mesh** apply a **Subdivision Modifier** and a **Simple Deform** to control its bending.

Then unwrapping the UVs like a simple **Soulercoaster**.

***Export without applying the modifiers.***


### HOUDINI IMPLEMENTATION

