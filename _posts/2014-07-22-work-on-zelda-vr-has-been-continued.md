---
id: 831
title: 'Work on Zelda VR has been continued'
date: '2014-07-22T23:36:25+02:00'
author: Shadow-Link
layout: post
guid: 'http://shadow-link.nl/?p=831'
permalink: /work-on-zelda-vr-has-been-continued/
categories:
    - 'Game Development'
    - Games
    - 'Oculus Rift'
    - VR
    - ZeldaVR
---

It’s been quiet a while since I last posted about Zelda VR. Summer is here and work kept me busy. After a long day of coding at the office I just didn’t feel like coding even more at home. So not much progress has been made until last week.

With the DK2 right around the corner I started getting hyped about VR again and decided it was time to get back to the project. First thing I had to do was update to the 0.3.x SDK (let’s hope the next version won’t mess up to much). Which surprisingly didn’t take that long due to the excellent examples and libraries floating around on GitHub. Once I got that out of the way I continues work on the main goal; Loading and emulating the Zelda ROM.

People might wonder why I am using the ROM as a base instead of ripping the assets from the original game and drop them in an engine like Unity or UDK like several other projects do. Let me explain why I take this approach:

**Legal issues.** One of the main main reason. Ripping models, sounds and other assets from a game and distributing them is not allowed. By loading all the assets from the ROM I try to bypass this and basically do the same as any other N64 emulator. With the only difference that my game will only work with one single game and contains a lot of custom code to fancy up the graphics and make everything VR compatible. For the user this means he needs to own a copy of the ROM and place that in the games folder.

**Learning something new.** It’s a challenge to get all this working. Especially because I’ve never tried to do something like this before, but have always been interested in Emulators and how they work.

**Amount of work.** The amount of work to get everything running is gigantic. I need to be able to emulate every part of the game. But doing it this way also has an upside, once you got one part working, for example loading one map, all maps will work. So instead of having to rip every single model, I’ll have to make sure I can load one map and all of them will automagically work. The same goes for the Actor scripts (all interactive elements in a map), audio and collisions.

That’s basically it. I hope you are as excited about this project as I am and maybe one day you’ll be able to play my favorite game in VR.