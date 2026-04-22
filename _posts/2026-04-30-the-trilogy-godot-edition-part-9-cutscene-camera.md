---
title: "The Trilogy: Godot Edition - Part 9 - Cutscene camera"
date: '2026-04-30T21:30:00+02:00'
author: Shadow-Link
layout: post
permalink: /the-trilogy-godot-edition-part-9-cutscene-camera/
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
serie_paging_name: Cutscene 2
---

## The camera data

Camera movement is stored in `bet.dat`. This is a plain text file, so let's open it up in a text editor.

```text
29,
0f,15.1893,15.1893,15.1893,
# 28 similar entries
;
12,
0f,0.0,0.0,0.0,
# 11 similar entries
;
44,
0f,-36.558,-27.5815,126.056,-36.558,-27.5815,126.056,-36.558,-27.5815,126.056,
# 43 similar entries
;
58,
0f,-32.1766,-27.5772,16.4855,-32.1766,-27.5772,16.4855,-32.3134,-27.5332,16.6541,
# 57 similar entries
;
;
```

The file is split up into sections, each section starts with a counter which indicates the amount of entries in that section. Each section ends with a `;`.

In total there are 4 sections: Zoom, Rotation, Position and Target.
- Zoom: The zoom level of the camera
- Rotation: Rotation of the camera
- Position: Position of the camera
- Target: The position the camera targets

```text
29,
0f,15.1893,15.1893,15.1893,
# 28 similar entries
;
```