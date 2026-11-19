---
title: "CatSpider"
date: 2026-08-17T14:14:00+08:00
draft: false
summary: "A spider-legged cat with a procedural gait built in Unreal Engine’s Control Rig."
cover: "CatSpider.gif"
---

# CatSpider

<img src="../../../projects/catspider/CatSpider.gif" width="800">

# Generating and preparing the model

The model generated with Hunyuan3D
<img src="../../../projects/catspider/image.png" width="800">

The model after cleanup
<img src="../../../projects/catspider/image%201.png" width="800">

# Rigging

I built a custom skeleton for the character.
<img src="../../../projects/catspider/image%202.png" width="800">

# Control Rig setup

<img src="../../../projects/catspider/image%203.png" width="800">

## Foot locking

### 1. Set the gait cycle

The legs need to swing faster as the body picks up speed, so I adjust the gait cycle based on movement speed.

1. Calculate the duration of a cycle at the current speed (`CycleLengthInSeconds`).

<img src="../../../projects/catspider/image%204.png" width="800">

2. Adjust how quickly the cycle advances.

<img src="../../../projects/catspider/image%205.png" width="800">

### 2. Update the booleans in FootLockedArray

- Compare `saturate(FootOffset[i] + CyclePercent)` with `SwingPercent`.
    - Move the foot during the swing phase and lock it for the rest of the cycle.
- The graph below updates the lock state for each foot.
<img src="../../../projects/catspider/image%206.png" width="800">

### 3. Update the foot position when it unlocks
<img src="../../../projects/catspider/image%207.png" width="800">

## Computing foot positions in world space

### 1. Predict stride length

First, choose where the foot should land.

PredictedFootTransforms = WorldFinalFootTransforms + Velocity * Something

<img src="../../../projects/catspider/image%208.png" width="800">

$$
\text{Something} =
\left[
S-p+\frac12(1-S)
\right]T
$$

- `S = SwingPercent` is the fraction of the cycle spent in swing.
- `p = PerFootCyclePercent` is this foot’s current progress through the cycle.
- `T = CycleLengthInSeconds` is the duration of a complete gait cycle.
- `v = Velocity` is the body’s world-space velocity.

The prediction looks ahead by two intervals.

$$
\underbrace{(S-p)T}_{\text{time left in swing}}
+
\underbrace{\frac12(1-S)T}_{\text{half the stance phase}}
$$

```text
0                  S                        S + ½(1-S)            1
|------ swing -----|-- first half of stance --|-- second half ----|
  current p        touchdown                  midstance
```

```text
Touchdown: the foot lands ahead of the body.
    ↓
Midstance: the body catches up and the foot is roughly underneath it.
    ↓
Just before liftoff: the body has passed the foot, leaving it behind.
```

### 2. Foot Lift

The vertical (Z) offset comes from a curve.

- X is the foot’s progress through swing.
- Y sets the lift height.

<img src="../../../projects/catspider/image%209.png" width="800">

### 3. Trace the ground at the landing point

<img src="../../../projects/catspider/image%2010.png" width="300">

Trace vertically through the predicted landing point and place the foot at the hit position.

<img src="../../../projects/catspider/image%2011.png" width="800">

An improved version of the trace setup

<img src="../../../projects/catspider/image%2012.png" width="300">

## Updating the pose

Apply Full Body IK to the updated foot targets.

<img src="../../../projects/catspider/image%2013.png" width="800">
