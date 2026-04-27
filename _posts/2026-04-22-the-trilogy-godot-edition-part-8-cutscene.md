---
title: "The Trilogy: Godot Edition - Part 8 - Cutscene"
date: '2026-04-22T19:30:00+02:00'
last_updated: '2026-04-27T06:40:00+02:00'
author: Shadow-Link
layout: post
permalink: /the-trilogy-godot-edition-part-8-cutscene/
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
serie_paging_name: Cutscene 1
---

> _Sorry babe, I'm an ambitious girl and you, you're just small time._

In this part of the series we'll take a look at how cutscenes are handled. We'll skip the animation implementation for now, as I haven't figured out the final details on how I want to import them into Godot yet.

Cutscenes in GTA are all rendered in real time in engine. You might have never seen them, but the locations that are used in cutscenes all exist somewhere on the map. 

For example the famous intro cutscene of GTA: III happens around here, cleverly hidden behind the mountains:

![Ghost town location](/assets/images/the-trilogy-godot-edition/cutscene-gta3-ghosttown.png)

And GTA: VC's intro cutscene actually plays inside the Ocean View Hotel. Hidden by Vice Cities new interior system.

## The script
To see how those cutscenes are set up we'll have to dive into the source of the mission script.

If we take a look at GTA: III `intro.sc` file, we see the following lines:
```
// **********************************START OF BANK CUTSCENE****************************
MAKE_PLAYER_SAFE_FOR_CUTSCENE Player

SET_INTRO_IS_PLAYING TRUE

LOAD_COLLISION LEVEL_GENERIC
LOAD_SPECIAL_CHARACTER 1 cat
LOAD_SPECIAL_CHARACTER 2 colrob
LOAD_SPECIAL_CHARACTER 3 miguel
LOAD_SPECIAL_CHARACTER 4 playerx
LOAD_SPECIAL_MODEL cut_obj1	cs_ban
LOAD_SPECIAL_MODEL cut_obj2 bankd
LOAD_SPECIAL_MODEL cut_obj3	cs_loot
LOAD_SPECIAL_MODEL cut_obj4	colt1
LOAD_SPECIAL_MODEL cut_obj5	cath
```

We'll go into the details of the scripting language in another post (there is so much stuff to write about for this game!), for now let's go over these _opcodes_ one by one.

- `MAKE_PLAYER_SAFE_FOR_CUTSCENE Player` makes sure that nothing happens to the player during the cutscene. This prevents things like the player dying during the cutscene. 
- `SET_INTRO_IS_PLAYING` sets a flag indicating that the intro is playing, we don't know what this does exactly, but I assume other pieces of the engine use this to determine if the intro is playing. 
- `LOAD_COLLISION` loads collision data.
- `LOAD_SPECIAL_CHARACTER 1 cat` loads the character model `cat` into special character slot `1`.
- `LOAD_SPECIAL_MODEL cut_obj1	cs_ban` loads `cs_ban` into cutscene object slot `cut_obj1`.

Let's skip a little bit further in the script to the actual cutscene stuff:

```
LOAD_CUTSCENE bet
LOAD_SCENE -559.65 1030.56 40.0

SET_CUTSCENE_OFFSET -537.42 1051.204 36.884

CREATE_CUTSCENE_OBJECT PED_SPECIAL4 cs_player
SET_CUTSCENE_ANIM cs_player playerx

// More cutscene object setup

CREATE_CUTSCENE_HEAD cs_cat cut_obj5 cs_cathead
SET_CUTSCENE_HEAD_ANIM cs_cathead cat

// More cutscene object setup

START_CUTSCENE
```

Again let's go over the opcodes one by one.

- `LOAD_CUTSCENE` Loads the cutscene data from `anim/cuts.img`, this includes: 
  - `bet.ifp` the key frame animation data
  - `bet.dat` the camera movement data
  - `bet_cat.anm` Catalina's head animation data
  - `bet.mp3` from the audio directory
- `LOAD_SCENE` Tells the engine to load the scene at a specific location
- `SET_CUTSCENE_OFFSET` Cutscene data is based on a local coordinate system (0.0, 0.0, 0.0). To play the cutscene at the correct location an offset is applied.
- `CREATE_CUTSCENE_OBJECT PED_SPECIAL4 cs_player` Creates a new cutscene object with model `PED_SPECIAL4` stored in variable `cs_player`
- `SET_CUTSCENE_ANIM cs_player playerx` Applies the `playerx` animation from `bet.ifp` to the `cs_player` cutscene object
- `CREATE_CUTSCENE_HEAD cs_cat cut_obj5 cs_cathead` Creates the `cath` head object on the `cs_cat` cutscene object and stores it in `cs_cathead`
- `SET_CUTSCENE_HEAD_ANIM` Applies the `cat` animation from `bet_cat.anm` to Catalina's head.
- `START_CUTSCENE` Starts the cutscene.

That's quite some setup to play a single cutscene! To replicate the cutscene we have to do the same steps in Godot. In the next few posts I'll describe the steps to get this cutscene playing.

## The map

First of all we have to make sure the map is loaded, the intro cutscene is located at `-559.65 1030.56 40.0` which should load if we load the map data from the `landsw` directory.

![Intro cutscene map](/assets/images/the-trilogy-godot-edition/cutscene-intro-1.png)

Rendering is a bit off, but it's good enough for now! 

In the next post we'll take a look at camera movement data found in `bet.dat`.