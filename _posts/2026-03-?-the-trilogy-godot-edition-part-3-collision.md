---
title: The trilogy Godot Edition - Part 2 - Collision
date: '2026-03-?T18:00:00+02:00'
author: Shadow-Link
layout: post
permalink: /the-trilogy-godot-edition-part-3-collision/
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
serie_paging_name: 3
---
With some basic model loading working (no worries we'll get to the textures at some point!) it might be nice to look at something completely different; Collision!

__What do I mean with collision?__

The models we loaded up until now are only used for the visual representation of an object. The chair we loaded might look physical, but if someone would try to sit on it, they would fall through. The reason for this is that it's lacking a physical model aka a collision model. A collision model defines the shape, and in case of GTA the material, of the model. We use the collision model to define the roads we drive on and the walls we bump into.

__Why do we need separate collision models?__ 

Physics are complex, even though we have amazing physics engines and our computers can compute millions of physic interactions per second, simulating everything using their visual representation would be impossible. The visual representation of a model is usually much more detailed than necessary for believable physics simulation.

