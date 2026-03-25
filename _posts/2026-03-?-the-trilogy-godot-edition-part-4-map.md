---
title: The trilogy Godot Edition - Part 4 - Map
date: '2026-03-?T11:00:00+02:00'
author: Shadow-Link
layout: post
permalink: /the-trilogy-godot-edition-part-4-map/
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
serie_paging_name: Map Part 1
---
Now that we have model and collision loading in place. Let's put it all together and take a look at how the meshes are placed to create our beloved cities.

One of the first things the games load are the following dat files; `default.dat` and `gta(game version).dat`. These dat files are simple text files that tell the engine which file to load.

Let's open up Vice City's `default.dat` and go through the file step by step.

```
# 
# Load IDEs first, then the models and after that the IPLs
# 
```

The first couple of lines start with a `#`. This could be familiar to Godot devs as these are just comments. The engine ignores any line that starts with a `#`.

Let's read a little bit further, the first non comment line is:
```
IDE DATA\DEFAULT.IDE
```

Now it starts to get interesting. So what does this line mean? We can split it up into two parts; `IDE` and `DATA\DEFAULT.IDE`. `IDE` is the command that tells the engine to load an IDE file als known as `Item DEfinition`, `DATA\DEFAULT.IDE` is the relative path of the ide file that should be loaded.  We'll get back to IDE files a little bit later.

Next up we see the following lines (skipping the comments).

```
TEXDICTION MODELS\MISC.TXD
MODELFILE MODELS\GENERIC\AIR_VLO.DFF
COLFILE 0 MODELS\COLL\VEHICLES.COL
```

Again this tells the engine to load specific file types. 
- `TEXDICTION` Loads a texture dictionary aka a collection of Textures. 
- `MODELFILE` [Loads a model](2026-03-12-the-trilogy-godot-edition-part-1-model-loading.md) 
- `COLFILE` [Loads a collision file](2026-03-25-the-trilogy-godot-edition-part-3-collision.md).

That's it for `default.dat`. Let's also open `gta.dat` or in Vice City's case `gta_vc.dat`.

This file is pretty similar to `default.dat`, it contains a bunch of `IDE` commands, but it does contain two new commands:

```
SPLASH loadsc2
IPL DATA\MAP.ZON
```

- `SPLASH` Switches the splash screen during loading. _Fun fact_: this only works on the console versions of the game.
- `IPL` Loads an IPL file also known as a `Item PLacement`. Again we'll take a look at those specific files in a bit.

If we take a look at both GTA: III and SA there are a couple more commands that are not used in Vice City.

- `IMG` Loads an `Image` archive file
- `MAPZONE` Loads a zone file in GTA: III. Seems to have been replaced with a regular IPL file in the later games.