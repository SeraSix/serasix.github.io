---
title: "第十一届世界渲染大赛"
date: 2026-03-15T0:15:00+08:00
draft: false
summary: "My first full pipeline animation project"
cover: "cover.jpg"
---

## 概览
<img src="wrc11.gif">  

## 细节拆解

### 建模

人物建模

<!-- ![s1front.png](f02a28dd-efe1-4cdb-b69a-8748b98666db.png)
![s1side.png](s1side.png)
![s1back.png](s1back.png)
![s2front.png](s2front.png)
![s2side.png](1e19f5c8-c390-4019-b029-c4c1afff248d.png)
![s2back.png](s2back.png)
![uv.png](uv.png) -->

<div style="display: grid; grid-template-columns: repeat(3, 2fr); gap: 16px;">
  <img src="f02a28dd-efe1-4cdb-b69a-8748b98666db.png">
  <img src="s1side.png">
  <img src="s1back.png">
  <img src="s2front.png">
  <img src="1e19f5c8-c390-4019-b029-c4c1afff248d.png">
  <img src="s2back.png">
</div>

uv 拆分：
![uv.png](uv.png)

### 人物绑定与动画

人物骨骼：rigify + 自建骨骼

<!-- ![s1rig.png](s1rig.png)
![s2rig.png](s2rig.png) -->

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="s1rig.png">
  <img src="s2rig.png">
</div>

动物：自建骨骼绑定 + 形态键

<p align="center">
  <img src="animals.gif">
</p>
 

### 几何节点

玉米地

- 利用空游标与网格面的插值做动画
- 根据距离改变大小以达到“生长”

![image.png](image.png)

## 后记

第一次全流程动画的尝试，没想到建模技术只有3岁宝宝走路实力的我和只有 8G 内存的 mac 可以合作出这样的作品，期间被 blender 暴击多次，但最后看着序列帧一帧一帧渲染出来的时候真的很开心！

![frame.png](frame.png)

这个作品的灵感几乎可以用下面这张图全部概括，25年暑假f1电影热映，而我还在练车场里思考如何才能不撞墙
<p align="center">
  <img src="reason.jpg" width="400">
</p>

东北有很多驾校在农村，练车时两边是一望无际的玉米地，有时早上能遇到农民带着羊群牛群遛弯。我的车技不好，但我能轻松超越小动物。大概是基于这个产生了 “穿越去动物世界比赛” 的想法

<!-- ![field2.jpg](field2.jpg)
[https://www.notion.so](https://www.notion.so) -->

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="field2.jpg">
  <img src="field3.jpg">
</div>


值得一提的是，我本来以为我的 lowpoly 大作难以入各大社交媒体的法眼，没想到以摆烂的心态发布后竟然收获了很多暖心的评论，小红书真是一个美好的地方

<!-- ![comment1.jpg](comment1.jpg)
![comment2.jpg](comment2.jpg) -->

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="comment1.jpg">
  <img src="comment2.jpg">
</div>