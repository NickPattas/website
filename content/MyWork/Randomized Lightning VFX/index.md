---
title: "Randomized Lightning VFX - Personal Project"
showReadingTime: false
showDate: false
showWordCount: false
orderBy: "weight"
weight: 2
---

Software used:
* Unreal Engine 5.7
* Embergen

In this personal project I wanted to create a system that allows the user to generate randomized lightning strikes on a 2D cloud image.

I wanted the effect to look realistic and powerful, suitable for environment effects and skies.

{{< youtube yqedelWJVEk >}}

I created a cloud texture using Embergen and rendered it with a three point light system.

![](assets/img/20251218114025.png)

The first texture (T_Cloud) was used to colorize the cloud inside Unreal Engine 5.7.

![](assets/img/20251218114123.png)

The other three textures were RGB lights in random positions and were used to drive the whole lightning effect.
![](assets/img/20251218114152.png)

I created a texture in a render target with random colors using Niagara's Grid 2D system.
![](assets/img/20251218113854.png)
![](assets/img/20251218121325.png)
![](assets/img/20251218121437.png)
![](assets/img/20251218113945.png)

Then, inside the Cloud's shader I created a logic that switches between each color of the render target with random timing.
![](assets/img/20251218114312.png)
![](assets/img/20251218114239.png)

This way, by randomizing both the render target's colors and the pattern that they are changing inside the material, I created emissive masks for the cloud that create the illusion of lightning strikes on a brewing storm.

{{< button href="https://nickpattas.com/posts/astudyonchaos/" target="_blank" >}}
Read the complete breakdown
{{< /button >}}