---
title: The trilogy Godot Edition - Part 4 - Map files
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

## DAT

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

## IDE

The Item Definition file contains as it name might give away; definitions of items. In all seriousness, the file defines the ID of a model, the TXD it uses and a bunch of other properties depending on the type of the item.

To clear things up, lets checkout `default.ide`, which is also the first file that got loaded by `default.dat`.

Again we start the file with a bunch of comments as indicated by `#`. We can probably skip this explanation next time ;), but do take a look at the comments in the file they contain useful info left by the devs.

Besides the comments, the structure of the file is slightly different from the `.dat` files we looked at previously. Instead of each line being a command that gets executed this file is split up into sections. Section starts are marked by specific keywords identifying the type of items in that section and the ending is marked by `end`.

With that out of the way lets have a look the file:
```
objs
# wheels
160, wheel_sport, generic, 2, 20, 70, 0
# Other entries
end
```

The `objs` keyword is the start marker of a section. In this case the `Objects` section. This section defines regular object aka models.

If we look at the first entry we see: `160, wheel_sport, generic, 2, 20, 70, 0`. 
Lets break it down:
- `160` is the ID of the model, this is a unique ID that is used by the engine to reference this model
- `wheel_sport` is the name of the DFF (aka a model)
- `generic` is the name of the TXD (aka the texture archive)
- `2` the amount of meshes in this model
- `20` the draw distance of the first mesh
- `70` the draw distance of the second mesh
- `0` some flags that set special rendering options

So now if the engine is told to load model `160` it will know which model to use, what texture archive to apply and how to render it.

We can go very in depth into every section but for now I'll give a short summary.
- `hier` Cutscene objects
- `cars` Vehicle definitions
- `peds` Pedestrian definitions

The next couple of sections are not found in `default.ide` but are used by the game in other `ide` files:
- `tobj` Timed objects, spawned only at specific times
- `path` Used to define paths for vehicles and pedestrians
- `2dfx` 2D effects, like lights
- `weap` Weapon models
- `anim` Animated objects
- `txdp` Texture archive extensions

## IPL