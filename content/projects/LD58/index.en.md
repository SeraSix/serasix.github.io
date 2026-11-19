---
title: "LD58: HeartKeys"
date: 2026-03-14T20:39:00+08:00
draft: false
summary: "I led the art team and handled technical art for HeartKeys, our Ludum Dare 58 entry."
cover: "cover.png"
---

## Overview

I was the lead artist and technical artist on our team for Ludum Dare 58. We finished in 19th place.

[Play HeartKeys in your browser](https://ldjam.com/events/ludum-dare/58/heart-keys)

![image.png](image.png)

Credits and final results (my name is highlighted below)

<img src="../../../projects/ld58/image%201.png" width="400">
<img src="../../../projects/ld58/image%202.png" width="400">

## Technical breakdown

**My roles:** lead artist and technical artist.

I coordinated the art team’s work and handled the technical side of the 3D assets.

### Third-person character animation

A fixed camera frames the player, and an animation state machine controls the character’s movement.

![image.png](<image 3.png>)

[Character movement controller source code](https://github.com/SeraSix/Unity_Reusable/blob/main/3rdPerson/Move_Controller.cs)

### Character modeling, rigging, and animation

<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px;">
  <img src="../../../projects/ld58/Pasted_image_20251005162424.png">
  <img src="../../../projects/ld58/Pasted_image_20251005162549.png">
  <img src="../../../projects/ld58/Pasted_image_20251005163547.png" >
</div>

![Pasted image 20251001112707.png](Pasted_image_20251001112707.png)

Unity Avatar setup

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 0px;">
  <img src="../../../projects/ld58/animation.gif">
  <img src="../../../projects/ld58/animation-.gif">
</div>

### Input System

I configured the input actions and wrote the [character controller](https://github.com/SeraSix/Unity_Reusable/blob/main/3rdPerson/Move_Controller.cs).

![image.png](<image 4.png>)

## Modeling the environment and props

A wide shot of the scene and some close-ups follow.

![overview.png](overview.png)

<p align="center">
  <img src="../../../projects/ld58/details2.png" width="500">
</p>

<p align="center">
  <img src="../../../projects/ld58/details1.png" width="500">
</p>

<p align="center">
  <img src="../../../projects/ld58/details3.png" width="500">
</p>

## Looking back

This was the game I made after a year of practice following LD56. We went for a bright, low-poly look that felt comforting. We placed much higher than I expected, and it was lovely to hear how much people enjoyed it.

![image.png](<image 5.png>)

The biggest challenge was coordinating a large art team entirely online. After spending the first day arguing, we gradually figured out a division of work that suited everyone. For the next jam, I’d like to get better at talking things through with the game designers…

<p align="center">
  <img src="../../../projects/ld58/367732ab309641df356fab5575299b89.jpg" width="200">
</p>

A few details from the level design are worth sharing.

In HeartKeys, each key stands for finding your way through a moment of uncertainty as you grow up. That idea also runs through the main loop: collect new abilities and use them to solve puzzles. We built three levels around school, family, and love. Completing them opens the final level, the future.

We half-buried enormous objects in sand to suggest the character’s inner turmoil. The idea came from a still in [a video by Koala on Bilibili](https://www.bilibili.com/video/BV1Wju1zrE2q/?spm_id_from=333.1387.upload.video_card.click).

![image.png](<image 6.png>)

The family level took a different direction. The designers felt strongly that the buried objects made it too hard to see where to go. We ended up with a tidy, empty two-bedroom apartment. I think its emptiness captured something about being a teenager and feeling misunderstood at home.

![image.png](eacd795f-28b2-498c-b8ea-8d9e1d32340f.png)

My favorite part of the love level is the gathering of roses and swords. The inspiration was a Georgian hillside covered in swords, pictured on the right. The story goes that a small army won a battle there against a much larger force a thousand years ago. The swords became a tribute to their courage.

That’s roughly how teenage love feels to me: the impulse to risk absolutely everything. My teammates took one look at the roses and swords and decided I must have had a very dramatic emo phase.

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px;">
  <img src="../../../projects/ld58/f45b54e4-d989-4aaf-beaf-e9c7a68246b7.png">
  <img src="../../../projects/ld58/image%207.png">
</div>

We chose low poly partly because time was short and I still had plenty to learn. It also helped that I love *Dancing Line*. (Thank you, *Dancing Line*!)

That’s about it. Here’s the team who made the game!

![image.png](<image 8.png>)
