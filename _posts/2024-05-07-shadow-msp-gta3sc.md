---
title: Shadow-MSP gets gta3sc support
date: '2024-05-07T08:10:00+02:00'
author: Shadow-Link
layout: post
permalink: /shadow-msp-gets-gta3sc-support/
categories:
    - Modding
    - Games
tags:
    - games
    - modding
    - gta
    - gta3sc
    - shadow-msp
---
I already mentioned in my previous post, but I am tired of the Chip-8 on N64 project... I got distracted once again.

This time by an old favorite of mine; Shadow-MSP. The Intellij plugin that I build to support GTA 3D mission scripting. 

A couple of years ago the original mission script sources got leaked (thanks Grovestreet games!) which helped understand the original SCM structure. [TheLink2012](https://github.com/thelink2012/) build an amazing toolchain and compiler called [gta3sc](https://github.com/thelink2012/gta3sc). This can be used to compile the original sources to the main.scm as we know it.

There is a plugin for [VSCode](https://github.com/thelink2012/vscode-gta3script), but nothing for Intellij. Luckily I already had a plugin lying around for exactly this purpose, mission script support in Intellij. So I [started adding support](https://github.com/KilianSteenman/Shadow-MSP/pull/43) for the original GTA 3D scripting languages using gta3sc as the compiler.

Of course, we are not there yet; the plugin is very slow, and it's missing some key features like compiling. Features I am working on as we speak. Expect more details soon!