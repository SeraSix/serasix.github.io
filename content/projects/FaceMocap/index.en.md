---
title: "Facial Motion Capture in Unreal Engine"
date: 2026-03-18T3:07:00+08:00
draft: false
author: "Sera"
summary: "A facial capture workflow using Live Link and ARKit to drive a custom character in Unreal Engine."
cover: "FinalEffect.gif"
---

## Overview

The final performance

<img src="../../../projects/facemocap/FinalEffect.gif">

The capture pipeline

![image.png](image.png)

## Modeling and rigging the face

<!-- ![ModelingFront.png](ModelingFront.png)
![ModelingSide.png](ModelingSide.png) -->

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="../../../projects/facemocap/ModelingFront.png">
  <img src="../../../projects/facemocap/ModelingSide.png">
</div>

I rigged the face with the Faceit facial armature.

<!-- ![FaceRig1.png](FaceRig1.png)
![FaceRig2.png](FaceRig2.png) -->

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="../../../projects/facemocap/FaceRig1.png">
  <img src="../../../projects/facemocap/FaceRig2.png">
</div>

## Painting skin weights

I refined the weights while testing individual poses, including an open mouth, a smile, and a downward gaze.

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="../../../projects/facemocap/MouthOpen2.png">
  <img src="../../../projects/facemocap/Smile.png">
  <img src="../../../projects/facemocap/EyeDown.png">
  <img src="../../../projects/facemocap/MouthOpen.png">
</div>

## Creating shape keys

I created the 52 ARKit facial shape keys.
<p align="center">
  <img src="../../../projects/facemocap/ShapeKeys.png" width="400">
</p>

Here are some of the shapes in motion.

The six clips show the eyes, nose, cheeks, and mouth.
<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="../../../projects/facemocap/EyeRoll.gif">
  <img src="../../../projects/facemocap/EyeBlink.gif">
  <img src="../../../projects/facemocap/Nose.gif" >
  <img src="../../../projects/facemocap/Blow.gif">
  <img src="../../../projects/facemocap/MouthMove1.gif">
  <img src="../../../projects/facemocap/MouthMove2.gif" >
</div>

## Reading and applying Live Link data

Once the model was ready, I imported it into Unreal Engine. The animation data takes the following path.

```text
Live Link Source
↓
LiveLinkRemapAsset
(remap curve names and values)
↓
Animation Blueprint
(read animation curves)
↓
Set Morph Target
↓
Character expression
```

### Reading the live data

I used Unreal Engine’s MetaHuman capture input to read 260 curve values in real time.

<p align="center">
  <img src="../../../projects/facemocap/image%201.png" width="400">
</p>

### Driving the shape keys in real time

- From the 260 input values, I chose the closest match for each of the 52 ARKit shapes. Here’s a test of the mapping.
<p align="center">
  <img src="../../../projects/facemocap/image%202.png">
</p>

- I used a list of objects to simplify the setup for the 52 shapes.
- For debugging, I grouped the shapes by the part of the face they affect: left, center, or right.

![AnimBP1.png](AnimBP1.png)

The table shows the mapping for paired shapes, using the left side as the example.

| ARKit / Faceit | MetaHuman Curve |
| --- | --- |
| browDownLeft | CTRL_expressions_browDownL |
| browOuterUpLeft | CTRL_expressions_browRaiseOuterL |
| cheekSquintLeft | CTRL_expressions_eyeCheekRaiseL |
| eyeBlinkLeft | CTRL_expressions_eyeBlinkL |
| eyeLookDownLeft | CTRL_expressions_eyeLookDownL |
| eyeLookInLeft | CTRL_expressions_eyeLookRightL |
| eyeLookOutLeft | CTRL_expressions_eyeLookLeftL |
| eyeLookUpLeft | CTRL_expressions_eyeLookUpL |
| eyeSquintLeft | CTRL_expressions_eyeSquintInnerL |
| eyeWideLeft | CTRL_expressions_eyeWidenL |
| mouthDimpleLeft | CTRL_expressions_mouthDimpleL |
| mouthFrownLeft | CTRL_expressions_mouthCornerDepressL |
| mouthLowerDownLeft | CTRL_expressions_mouthLowerLipDepressL |
| mouthPressLeft | CTRL_expressions_mouthPressDL |
| mouthSmileLeft | CTRL_expressions_mouthCornerPullL |
| mouthStretchLeft | CTRL_expressions_mouthStretchL |
| mouthUpperUpLeft | CTRL_expressions_mouthUpperLipRaiseL |
| noseSneerLeft | CTRL_expressions_noseWrinkleL |

These shapes have no separate left and right versions.

| ARKit / Faceit | MetaHuman Curve |
| --- | --- |
| browInnerUp | CTRL_expressions_browLateralL |
| cheekPuff | CTRL_expressions_mouthCheekBlowL |
| jawForward | CTRL_expressions_jawFwd |
| jawLeft | CTRL_expressions_jawLeft |
| jawOpen | CTRL_expressions_jawOpen |
| jawRight | CTRL_expressions_jawRight |
| mouthClose | CTRL_expressions_mouthLipsPurseUL |
| mouthFunnel | CTRL_expressions_mouthFunnelUL |
| mouthLeft | CTRL_expressions_mouthLeft |
| mouthRight | CTRL_expressions_mouthRight |
| mouthPucker | CTRL_expressions_mouthLipsPurseUR |
| **mouthRollLower** | CTRL_expressions_mouthLowerLipRollInL |
| **mouthRollUpper** | CTRL_expressions_mouthUpperLipRollInL |
| mouthShrugLower | CTRL_expressions_jawChinRaiseDL |
| mouthShrugUpper | CTRL_expressions_jawChinRaiseUL |
| tongueOut | CTRL_expressions_tongueOut |

### Driving head rotation

I read `HeadRoll`, `HeadPitch`, and `HeadYaw` to drive the skeletal animation.

![AnimBP2.png](AnimBP2.png)
