---
title: 2023 what a year!
date: '2023-12-21T22:00:00+02:00'
author: Shadow-Link
layout: post
permalink: /2023-what-a-year/
categories:
    - Games
tags:
    - games
---

The holiday season has started, and we are nearing the end of the year. Which is always a good time to look back at the previous year!

You might have noticed that I've been a bit more active since March 2023. That's the moment I challenged myself into writing a post at least once a month. This also explains the random [Pocket Ball](/games/pocket-ball) post from November ;). 

2023 has been an interesting year, I've worked on many projects and became a proud dad once again.

_Let's talk about some of the Highlights._

## Retro Trophies 64

I've always been nostalgic for retro games, with the N64 era in particular. But whenever I replay the old games I miss a sense of achievement. This gave me the idea to implement a trophy system for the [N64 Everdrive](https://krikzz.com/our-products/cartridges/ed64x7.html). 

I dived into the N64 homebrew scene and discovered the amazing [libdragon](https://github.com/DragonMinded/libdragon) SDK, which makes interacting with the [Everdrive](https://krikzz.com/our-products/cartridges/ed64x7.html) SD card (which contains save data) a breeze. 

Now all I had to do was figure out the save format of the games, luckily the N64 didn't have much storage space which made the saves pretty easy to bi-sect and in some cases this was already done by others. I've shared my research on GitHub in the [N64 save file repository](https://github.com/KilianSteenman/N64-Save-file-formats).

After a few weeks of research and coding I released the first version of [Retro Trophies 64](https://github.com/KilianSteenman/Retro-Trophies-64).

## OASE Engine

I've mentioned [OASE](https://www.shadow-link.nl/games/oase/) for the first time ever on my blog. OASE is my custom engine implementation of GTA: Vice City. 

I didn't take enough time to work on this project this year. The changes I did make where minor; tweaked the start menu and added loading / saving of the original settings file.

## Model viewer

I took a step back from the engine and decided to rewrite some of the model loading and rendering code from scratch. This gave me the opportunity to fix some of the design issues I made in the past which blocked a lot of innovation in OASE.

## Personal life

I became a proud dad of a beautiful baby girl. She's the reason I haven't been able to work on my projects as much, but it's all worth it. Waking up and seeing a big smile on her face when I get her out of bed is the best thing someone can imagine. <3