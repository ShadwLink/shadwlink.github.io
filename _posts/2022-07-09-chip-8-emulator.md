---
title: 'Kotlin Multiplatform Chip-8 Emulator'
date: '2022-07-09T12:00:00+02:00'
author: Shadow-Link
layout: post
permalink: /chip-8-emulator/
categories:
- Games
---

I've been wanting to do something with Kotlin Multiplatform for a while now but couldn't think of a nice project.
As I've been interested in the world of emulation for a while, I thought it could be a nice challenge to create the "
hello world" of emulators, the 'Chip-8', using Kotlin Multiplatform.

The first working version of the emulator is now available on my GitHub https://github.com/KilianSteenman/KEmulation.
The emulator works (without sound) on Android, Desktop and Web.

As much as I love Kotlin, writing an emulator was still annoying due to the lack of proper Unsigned types (Thanks Java!)
. The experimental unsigned types implementation is just not that great to work with. Besides that it still feels like
early days for Multiplatform, the setup is just not as straightforward and documentation is outdated or lacking.

Anyway I don't expect to spend much more time on the emulator as it's pretty much finished. On to the next coding
challenge!