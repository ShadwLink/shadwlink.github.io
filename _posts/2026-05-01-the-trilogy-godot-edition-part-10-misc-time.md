---
title: "The Trilogy: Godot Edition - Part 10 - Misc time"
date: '2026-05-01T07:42:00+02:00'
author: Shadow-Link
layout: post
permalink: /the-trilogy-godot-edition-part-10-misc-time/
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
serie_paging_name: Time
---

It's time for... time. All puns aside, to get the right vibe in the cutscene, we'll have to adjust the time of day and weather. Now the weather in GTA is time based, so we'll take a look at the time first.

GTA uses a 24-hour clock, but time in the GTA world goes by a lot, and I mean a lot, faster than in the real world. Which is a good thing, as we don't want to wait a full day to be able to play that one mission that can only be started at 6:00 in the morning.

So how much faster is it? Every in game hour takes one real life minute, which means a full in game day takes only 24 minutes!

Let's implement a basic in game clock. First we create a new `Node` and add a script called `Time`.