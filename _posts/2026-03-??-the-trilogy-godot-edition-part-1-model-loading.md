---
title: The trilogy Godot Edition - Part 1 - Model loading
date: '2026-03-??T20:00:00+02:00'
author: Shadow-Link
layout: post
permalink: /the-trilogy-godot-edition-part-1-model-loading/
categories:
  - Modding
  - Games
tags:
  - games
  - modding
  - gta
  - game-dev
  - godot
serie: the-trilogy-godot-edition
---
In this first part of the series we discuss model loading. Nothing more visual than rendering our first GTA model.

To load a GTA model we first need to understand the original engine this game used. The original trilogy was based on the [RenderWare engine](https://en.wikipedia.org/wiki/RenderWare) (RW from now on), an engine that was very popular during the time. Many games by different developers where created on this engine, think about titles like Burnout, Tony Hawks Pro Skated 3 and Bully. It was basically the Unreal Engine of that era.

Lucky for us this means [a lot](https://en.wikipedia.org/wiki/RenderWare#File_formats) is [known](https://gtamods.com/wiki/RenderWare_binary_stream_file) about the file formats used by RW based games. Entire tools and libraries where build to inspect the contents of RW files. One of which is called [RwAnalyze](http://steve-m.com/downloads/tools/rwanalyze/), this is still one of the best tools (22 years old by now!) to get a grasp of the basic structure of RW files.

![Screenshot of RW Analyze 0.4](assets/images/the-trilogy-godot-edition/rwanalyze.jpg)

As you can see in the above screenshot a dff file is basically a lot of 3D data stored in a tree like structure. The most interesting parts for us will be the `FrameList`, `Geometry` and `Material` sections.

__Framelist__

The framelist is a hierarchy of `Frames`. A Frame contains a position, rotation and parent Frame ID.

Frames can be mapped to geometry, bones or just be used as dummy placeholders to attach objects to at runtime.

__Geometry__

The geometry section contains data about the mesh; vertices, polygons, material mapping etc.

__Material__

The material section contains data about a material; the texture that is used, colors, alphas etc.

# Putting it all together
By creating a parser that reads the data sections mentioned above we should be able to import a dff file and convert it to something that is usable in Godot.

