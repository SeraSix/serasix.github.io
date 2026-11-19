---
title: "OpenWorld"
date: 2026-08-15T14:14:00+08:00
draft: false
summary: "A stylized open world with volumetric clouds and grass that bends as the player moves through it."
cover: "image.png"
---
# A stylized world with volumetric clouds

<img src="../../../projects/openworld/image.png" width="800">

# Volumetric clouds

<img src="../../../projects/openworld/%E8%87%AA%E5%AE%9A%E4%B9%89%E4%BD%93%E7%A7%AF%E4%BA%91.gif" width="800">

<img src="../../../projects/openworld/image%201.png" width="800">

### Sampling a 3D volume texture with wind

<img src="../../../projects/openworld/image%202.png" width="800">

$$
\mathbf{uvw} =
\frac{\mathbf{P}_{\mathrm{world}}}{S}
+
\mathbf{D}_{\mathrm{wind}}V_{\mathrm{wind}}t
$$

- $P_{world}$ is the world-space position of the current ray-marching sample.
- $S$ sets the spatial scale of the cloud noise.
- $D_{wind}$ is the wind direction.
- $V_{wind}$ is the wind speed.
- $t$ is time.
- $uvw$ gives the three coordinates used to sample the volume texture.

### Culling by height

<img src="../../../projects/openworld/image%203.png" width="800">

The height function is

$$
H(x)=(1−e^x)(1−e^{1−x})
$$

The custom material node evaluates it as follows.

```c
float x = saturate(NormAltitudeInLayer);

float a = 1.0 - exp(x);
float b = 1.0 - exp(1.0 - x);

return a * b;
```

The resulting density is computed as

$$
\rho =
\operatorname{saturate}
\left[
N-\left(1-H(h)\right)B
\right]
$$

- $N$ is the base 3D noise.
- $H(h)$ is the height-dependent density function.
- $B$ is the height bias.
- $ρ_{raw}$ is the raw density after the height adjustment.

# Interactive grass

## Blade color

<img src="../../../projects/openworld/image%204.png" width="800">

- At the base, sample the ground color from a render texture.
- At the tip, use a custom color.

## Bending the grass

The material uses `RotateAboutAxis` to bend each blade.

<img src="../../../projects/openworld/image%205.png" width="500">

- **Rotation axis:** take the cross product of the Z axis and the vector from the player to the grass.

<img src="../../../projects/openworld/image%206.png" width="500">

- **Pivot Point:** the base of the blade.
- **Position:** the absolute position.

### Computing the rotation angle

1. Record the player’s position by writing it to a render target (RT).

<div class="image-pair">
  <img src="../../../projects/openworld/image%207.png" alt="Writing the player position to the render target, step one">
  <img src="../../../projects/openworld/image%208.png" alt="Writing the player position to the render target, step two">
</div>

<img src="../../../projects/openworld/%E5%86%99%E5%85%A5_RT.gif" width="800" alt="The player position updating in the render target">

The Blueprint graph

<img src="../../../projects/openworld/image%209.png" width="800">
