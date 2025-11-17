In theatre it is common to create **visual effects** on stage by using shape masks to cast shadows across the scene. These masks are called **"cucoloris" or "cookies"**.

In Unity, a `cookie` is a **mask** that you place on a `Light` to create **a shadow with a specific shape or color**, which changes the appearance and intensity of the Light.

Cookies are an efficient way of simulating **complex lighting effect**s with **minimal or no runtime performance impact**. Effects you can simulate with cookies include caustics, soft shadows, and light shapes.

The cookies in Unity are used like Textures in Light Materials into Unreal Engine.

**The pixels of a cookie** does not need to be completely transparent or opaque, but can also incorporate any values in between.

For Universal [[Render Pipeline]] the texture format to use depends on the type of Light:
* Directional: 2D texture
* Spot: 2D texture
* Point: Cubemap texture

**Both for URP and HDRP the cookies can be colored (RGB)**
### Limitations
In the Built-In [[Render Pipeline]], **VertexLit** shaders can’t display Cookies or Shadows. Also, cookies only use data from the alpha channel. This means that you can define a shape for a cookie, but not a color.

Shadows are disabled for directional lights with cookies when forward rendering is used. It’s possible to write custom shaders to enable shadows in this case

### **Further Reading**

* https://docs.unity3d.com/6000.1/Documentation/Manual/creating-cookies-built-in-render-pipeline.html
* https://docs.unity3d.com/6000.1/Documentation/Manual/urp/light-component.html