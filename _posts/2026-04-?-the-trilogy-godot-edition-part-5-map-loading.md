---
title: The trilogy Godot Edition - Part 5 - Map loading
date: '2026-0?-?T11:00:00+02:00'
author: Shadow-Link
layout: post
permalink: /the-trilogy-godot-edition-part-5-map-loading/
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
serie_paging_name: Map Part 2
---
> ⚠️️
> A little disclaimer:
> 
> Godot currently doesn't provide streaming capabilities out of the box. But, the games we try to simulate are very old and hardware has improved immensely in the past 25(!) years. So we might actually get away with just rendering the map without implementing any streaming. 
> 
> For now, we'll take the most naive, non optimized, approach (remember I am not an expert at Godot nor at Game dev) and might improve our implementation at a later stage.
> 
> With that out of the way, let's get started!

## IPL Loading

The actual placement of objects is defined in IPL files. This file contains the location data of an object. Which means we should be able to display a bunch of boxes at the location data and already get a feel of the map. Let's go.

The easiest way to display a lot of boxes at certain positions is by just adding `MeshInstance3D` nodes to a scene, but this is a learning experience so we can do it a bit more efficiently. We can use `MultiMeshInstance3D`, a node specifically created to render repeating meshes efficiently, perfect for our use case!

Some example code, this assumes we have an IPL file loaded into memory that contains an array of instances.

```C#
// Create the multiMeshInstance3D node
MultiMeshInstance3D multiMeshNode = new MultiMeshInstance3D();

// Create a multi mesh
MultiMesh multiMesh = new MultiMesh
{
    TransformFormat = MultiMesh.TransformFormatEnum.Transform3D,    // Sets up our multimesh to support 3D transforms
    InstanceCount = ipl.Instances.Count,                            // Set the amount of instances to our IPL instance count
    Mesh = new BoxMesh                                              // Set the mesh to a simple box
    {
        Size = new Vector3(2.0f, 2.0f, 2.0f),
    }
};

// Loop through our IPL instances and set the transforms in the multimesh
for (var i = 0; i < ipl.Instances.Count; i++)
{
    var inst = ipl.Instances[i];
    multiMesh.SetInstanceTransform(i, new Transform3D(this.Basis, inst.Position));  // Set the transform to our instance position (Ignoring rotation and scale for now)
}

// Set the MultiMesh in our MultiMeshInstance3D node and add it to our scene
multiMeshNode.Multimesh = multiMesh;
AddChild(multiMeshNode);
```

The result:

![IPL instances loaded as boxes](/assets/images/the-trilogy-godot-edition/map-ipl-boxes.png)

Hmm something is up, and it's not Z! If you didn't get that joke no worries I'll explain it.

## The coordinate system

Godot and GTA use a different coordinate system! [Freya Holmer](https://bsky.app/profile/freya.bsky.social) created an amazing image that explains the difference in coordinate systems and it's usages.

![Coordinate system explained by Freya Holmer](/assets/images/the-trilogy-godot-edition/map-coordinate-system.jpg)

As you can see in the above image, Godot uses the `Right Handed` `Y-Up` coordinate system. But, which one does GTA use? Well the modeling / mapping tool used for the original trilogy was 3DS Max, which matches with the coordinate system used by GTA, the `Right Handed` `Z-Up` coordinate system.

There are multiple options to switch between those coordinate systems.
1. Swap the Y and Z values of every Vector3 when loading it into Godot.
2. Rotate every object individually
3. Rotate the camera
4. Rotate the world root node

And to be honest I am not sure what the best approach is. Option #1 sounds easy, but will probably end up causing issues when Z is not used in a Vector3 (IE: By the script) and might not work nicely with rotations. Option #2 sounds like a lot of work. So I guess that leaves us with options #3 and #4. For now, I'll use option #4 as that is the easiest.

After rotating the world 90 degrees we end up with, which already looks a lot better!
![Rotate world](/assets/images/the-trilogy-godot-edition/map-rotate-world.png)
