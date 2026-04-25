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

Let's have a look at all 4 sections. 

### Zoom

```text
29,
0f,15.1893,15.1893,15.1893,
# 28 similar entries
;
```

The 29 indicates that there are 29 'zoom' entries in this section. The next line is an entry. The first value 0f is the time into the cutscene when the entry happens, in this case the zoom is set to `15.1893` right at the beginning of the cutscene. For some reason the value is repeated 3 times, we can ignore the last 2. 

We can simulate the camera zoom by setting the camera FOV value.

### Rotation

```text
12,
0f,0.0,0.0,0.0,
```

Pretty much the same as zoom; 12 entries, first entry sets the camera rotation to 0.0 degrees at the beginning of the cutscene.

### Position

```text
44,
0f,-36.558,-27.5815,126.056,-36.558,-27.5815,126.056,-36.558,-27.5815,126.056,
```

And again, a similar format. 44 entries, each entry setting the position of the camera, and again the position is repeated 3 times.

### Target

```text
58,
0f,-32.1766,-27.5772,16.4855,-32.1766,-27.5772,16.4855,-32.3134,-27.5332,16.6541,
```

And surprise, surprise, the last section uses the same format. 58 entries with target position data. This is basically the direction the camera aims in.

## Animation player

With the data available, we can start with the implementation. We can use Godot's [AnimationPlayer](https://docs.godotengine.org/en/stable/classes/class_animationplayer.html) and  [Animation](https://docs.godotengine.org/en/stable/classes/class_animation.html) classes for this. First we'll have to convert the animation data to an Animation. Some pseudo code:

```C#
// Create new animation
Animation animation = new Animation();
// Set the loop mode to None as we only want to play the animation ones.
animation.LoopMode = Animation.LoopModeEnum.None; 
// Set the animation length to the full cutscene length
animation.Length = cameraPath.GetLength();

// Create the position data track
int positionTrackIndex = animation.AddTrack(Animation.TrackType.Position3D);
animation.TrackSetPath(positionTrackIndex, "CutsceneCamera");

// Now add all position entries to the position track
foreach (var positionData in cameraPath.PositionEntries)
{
    // Add a position key frame at each timestamp, the animation player will take care of interpolation
    animation.PositionTrackInsertKey(positionTrackIndex, positionData.Timestamp, positionData.Position);
}
```

With the animation ready we can now create an animation player that can actually play this animation.

```C#
// Create an animation library, this is required to play an animation using the animation player
AnimationLibrary cameraAnimLib = new AnimationLibrary();
// Add our cutscene camera animation to the librart
cameraAnimLib.AddAnimation("bet", animation);
// Add the animation library to the animation player
cameraAnimPlayer.AddAnimationLibrary("bet", cameraAnimLib);
// Set the newly created animation as the animation that needs to be played
cameraAnimPlayer.SetCurrentAnimation("bet/bet");
// Start playback
cameraAnimPlayer.Play();
```

The result:

// TODO: Insert result
