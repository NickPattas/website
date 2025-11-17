A compute shader is **a general-purpose GPU shader** that executes **independently of the** [[Render Pipeline]]. It is used to performing **heavy parallel computation** tasks that *may or may not involve graphics*.

**Runs once per thread in a grid (custom defined size)**

* Compute shaders are used for **general-purpose computing** tasks, often referred to as **GPGPU** (General-Purpose computing on Graphics Processing Units).

* Perform non-graphics tasks on the GPU, such as **physics simulations, image processing, AI operations, particle systems, data transformations, etc.**

* Written in shading languages like **GLSL**, **HLSL**, or **Metal Shading Language**.

* Launched via [[Dispatch Calls]] rather than [[Draw Calls]].

* Uses a grid of _work groups_ and _invocations_ (threads) to parallelize tasks.

#### Use Cases

- **Image filters** (blur, sharpen, edge detection)
- **Physics simulations** (fluids, cloth)
- **Matrix multiplications** for machine learning
- **Procedural generation** (terrain, noise)