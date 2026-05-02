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

It's time for... time. All jokes aside, to get the right vibe in the cutscene, we'll have to adjust the time of day and weather. Now the weather in GTA is time based, so we'll take a look at the time first.

GTA uses a 24-hour clock, but time in the GTA world goes by a lot, and I mean a lot, faster than in the real world. Which is a good thing, as we don't want to wait a full day to be able to play that one mission that can only be started at 6:00 in the morning.

So how much faster is it? Every in game hour takes one real life minute, which means a full in game day takes only 24 minutes!

Let's implement a basic in game clock. First we create a new `Node` and add a script called `Clock`.

// TODO: Add Clock code

## Mission script

Our clock can be adjusted by the mission script, with so-called opcodes. We are going to need methods for the following opcodes:
- [00BF: GET_TIME_OF_DAY](https://gtag.sannybuilder.com/opcode-database/opcode/00BF/)
- [00C0: SET_TIME_OF_DAY](https://gtag.sannybuilder.com/opcode-database/opcode/00C0/)
- [00C1: GET_MINUTES_TO_TIME_OF_DAY](https://gtag.sannybuilder.com/opcode-database/opcode/00C1/)
- [0253: STORE_TIME_OF_DAY](https://gtag.sannybuilder.com/opcode-database/opcode/0253/)
- [0254: RESTORE_TIME_OF_DAY](https://gtag.sannybuilder.com/opcode-database/opcode/0254/)

Out of scope for now as it's SA only:
- [088E: SET_TIME_ONE_DAY_FORWARD](https://gtag.sannybuilder.com/opcode-database/opcode/088E/)

That should be easy enough. Let's take a look at a possible way to implement those.

__GET_TIME_OF_DAY__

```C#
public void GetTimeOfDay(out int hour, out int minute)
{
    hour = GetHour();
    minute = GetMinute();
}
```

__SET_TIME_OF_DAY__

```C#
public void SetTimeOfDay(int hour, int minute)
{
    _hours = hour;
    _minutes = minute;
    EmitSignalOnTimeChanged(_hours, _minutes);
}
```

__GET_MINUTES_TO_TIME_OF_DAY__
```C#
public int GetMinutesToTimeOfDay(int targetHour, int targetMinute)
{
    int currentMinutes = _hours * 60 + _minutes;
    int targetMinutes = targetHour * 60 + targetMinute;

    return (targetMinutes - currentMinutes + 1440) % 1440;
}
```

__STORE_TIME_OF_DAY__
```C#
int _storedTimeOfDay = 0;

public void StoreTimeOfDay()
{
    _storedTimeOfDay = _hours * 60 + _minutes;
}
```

__RESTORE_TIME_OF_DAY__
```C#
public void RestoreTimeOfDay()
{
    _hours = _storedTimeOfDay / 60;
    _minutes = _storedTimeOfDay % 60;
    EmitSignalOnTimeChanged(_hours, _minutes);
}
```

And that's our clock for now! We will get back to it in the future to make some adjustments and add the missing SA opcode.