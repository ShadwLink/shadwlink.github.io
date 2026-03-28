---
title: "The Trilogy: Godot Edition - Part 4 - Map files"
date: '2026-03-27T11:00:00+02:00'
author: Shadow-Link
layout: post
permalink: /the-trilogy-godot-edition-part-4-map-files/
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

To get to that we need to understand the structure of the game files and how those contribute to the games map.

> ℹ️
> A lot of this info is based on the knowledge shared on [gtamods.com](https://www.gtamods.com)

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

Now it starts to get interesting. So what does this line mean? We can split it up into two parts; `IDE` and `DATA\DEFAULT.IDE`. In this example `IDE` is the command that tells the engine to load an IDE file also known as `Item DEfinition`, `DATA\DEFAULT.IDE` is the relative path of the ide file that should be loaded.  We'll get back to IDE files a little bit later.

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

That's it for the IDE file, lets see how these definitions are actually referenced by IPL files.

## IPL

The Item Placement files uses the exact same format as IDE files. It's a plain text file split up into sections.

If we open Vice City's `airport.ipl` in a text editor you'll see the following lines.

```
inst
865, ap_tower, 0, -1685.179443, -923.3638916, 13.48704815, 1, 1, 1, 0, 0, 0, 1
# More entries
end
```

Let's break it down again.

The section marker is `inst` short for _instance_. This section describes which models should be placed where.

Each entry has a lot of properties: `865, ap_tower, 0, -1685.179443, -923.3638916, 13.48704815, 1, 1, 1, 0, 0, 0, 1`

- `865` The ID as defined in IDE files
- `ap_tower` Model name (Not sure if this has any actual purpose as the model is also defined in the IDE)
- `0` The interior this model belongs to
- `-1685.179443` The X position
- `-923.3638916` The Y position
- `13.48704815` The Z position
- `1` The X scale
- `1` The Y scale
- `1` The Z scale
- `0` The X rotation (quaternion)
- `0` The Y rotation (quaternion)
- `0` The Z rotation (quaternion)
- `1` The W rotation (quaternion)

This is probably the most useful section of IPL files but lets list them all.

- `cull` Defines zones with some attributes
- `pick` Defines a pickup
- `path` Defines paths for vehicles
- `occl` Defines occlusion zones 

The following sections are San Andreas only:
- `grge` Defines a garage
- `enex` Defines entry and exit markers for interiors
- `cars` Defines a parked car generator
- `jump` Defines a stunt jump
- `tcyc` Something related to the timecycle
- `auzo` Defines an audio zone

## Next steps

With this knowledge of the IDE and IPL files we should already be able to create something that resembles a map!

We'll get to the implementation in the next post.
