---
title: "The Trilogy: Godot Edition - Intro"
date: '2026-03-10T20:00:00+02:00'
author: Shadow-Link
layout: post
permalink: /the-trilogy-godot-edition-intro/
categories:
  - Modding
  - Games
tags:
  - games
  - modding
  - gta
  - game-dev
  - godot
serie: The Trilogy Godot Edition
serie_paging_name: Intro
---

As mentioned in my last post (which I apparently posted over a year ago!) I've gotten interested in the awesome open
source game engine [Godot](https://godotengine.org).

In the past year I've done some simple projects with Godot, but now it's time to pick up something bigger. As you might
know I've worked on a project called [OASE](/games/oase/) in the past. This project aimed to create an Open Source
implementation of the GTA Trilogy. It was able to load the map and some missions pretty decently, but it always felt I
had to do everything from scratch, writing a graphics engine, an audio engine and all the other things that make up an
engine. The engine became a big mess, had a lot of memory issues (in the current state it basically crashes after
running for 30 seconds) and whenever I wanted to work on something I had to work my way through the spaghetti.
It's time to leave the OASE mess behind and create a new mess... in Godot.

__The goal: Get the GTA Trilogy running in Godot.__

Of-course we have multiple similar projects these days, one of which is a completely reverse engineered implementation,
which is basically the real deal and nothing can beat that. This project is not meant as a perfect recreation of the
trilogy, it's meant as a learning exercise, sharing my journey towards implementing a full 3D open world game (by 2001
standards).

__The plan__

The idea is to share the steps I take to get to a playable result. A step can be anything from loading models, playing
audio or scripting.

I'll be using code I've written for OASE as a basis. This means that I've got parsers ready for most of the file
formats. I might still go more in depth in the file formats when I use them in a post.

There are some things to keep in mind.

1. This is __not__ going to be a tutorial. The post will merely give you some ideas of how the GTA internals work (or at
   least how I interpret them) and how this can be applied in a modern engine like Godot.
2. This __won't__ be a one to one implementation, the goal is to get something playable, this probably means this will end
   up as the "We got GTA at home" version of the trilogy.
3. There are currently __no__ plans to open source this project.
4. There might __not__ be a logical order in these posts, switching from one topic to another is how my brain works and stays interested.
5. Last but not least, this project __won't__ be vibe coded. I want this to be a learning experience.

With all that said, I hope you are as excited about this as I am!

_Let the journey begin_