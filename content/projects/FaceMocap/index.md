---
title: "UE 面部捕捉实现"
date: 2026-03-18T3:07:00+08:00
draft: false
author: "Sera"
summary: "基于LiveLink + ARKit的面部捕捉流程"
cover: "cover.png"
---

## 概述：

效果：

<img src="FinalEffect.gif">  

核心流程：

![image.png](image.png)

## 面部建模与绑定

<!-- ![ModelingFront.png](ModelingFront.png)
![ModelingSide.png](ModelingSide.png) -->

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="ModelingFront.png">
  <img src="ModelingSide.png">
</div>


绑定工具：Faceit 脸部骨骼

<!-- ![FaceRig1.png](FaceRig1.png)
![FaceRig2.png](FaceRig2.png) -->

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="FaceRig1.png">
  <img src="FaceRig2.png">
</div>


## 刷权重

刷权重直至特殊动作形态正常

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="MouthOpen2.png">
  <img src="Smile.png">
  <img src="EyeDown.png">
  <img src="MouthOpen.png">
</div>

## 制作形态键

制作 ARKit 52 个形态键：
<p align="center">
  <img src="ShapeKeys.png" width="400">
</p>

效果如下：

插入6 个 GIF 图
<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="EyeRoll.gif">
  <img src="EyeBlink.gif">
  <img src="Nose.gif" >
  <img src="Blow.gif">
  <img src="MouthMove1.gif">
  <img src="MouthMove2.gif" >
</div>


## livelink 读入 + 控制

处理完之后将模型导入 UE，UE 中的操作流程大致如下：

```csharp
Live Link Source  
↓  
LiveLinkRemapAsset  
（改名字 / 改数值）  
↓  
Animation Blueprint  
（读取曲线）  
↓  
Set Morph Target  
↓  
角色表情
```

### livelink 读入数据

借用了 UE meta human 的读入功能，实时读入 260 个关键数据

<p align="center">
  <img src="image%201.png" width="400">
</p>

### 实时设置形态键的值

- 从 260 个值中选取最合适的值输给 52ARKit，测试效果如下：
<p align="center">
  <img src="image%202.png">
</p>

- 设置 52 个 ARKit + 用对象列表简化
- 为了便于调试我分成了左中右三个组

![AnimBP1.png](AnimBP1.png)

左 / 右部分对应表格如下:

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

无左右的形态键如下：

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

### 设置头部转动

核心：读取 HeadRoll / HeadPitch / HeadYaw 来控制骨骼动画

![AnimBP2.png](AnimBP2.png)