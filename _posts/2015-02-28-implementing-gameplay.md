---
id: 868
title: 'Implementing Gameplay'
date: '2015-02-28T10:46:22+01:00'
author: Shadow-Link
layout: post
guid: 'http://shadow-link.nl/?p=868'
permalink: /implementing-gameplay/
categories:
    - Games
---

The biggest challenge of Zelda64 VR is implementing the gameplay. We don’t want to reinvent the wheel and recode all the gameplay that can be found in Ocarina of Time. There are just to many big and small gameplay elements for that. Before I get into much technical detail I will explain how Ocarina of Time works.

Every object, every character and every item has its own piece of [code](http://spinout182.com/mqd/a.html). This piece of code is called the actor code. The actor code contains some basic information like the model that should be used to render this actor, the scale and much more. Besides this info there is also a piece of code that runs when the actor is active. For static object this can be as [small](http://vg64tools.googlecode.com/svn/n64/z_snippets/ovl_en_vase/ovl_en_vase.c) as a few lines. But for animated objects that the player can interact with, the code can be thousands of lines.

So why haven’t you seen any gameplay videos yet? The code I told you about is compiled [MIPS](http://en.wikipedia.org/wiki/MIPS_instruction_set) code. It’s not really easy to read and it takes a long time to build a program that runs the code properly. Besides that the code contains a lot of calls to functions that I don’t know the purpose of. There is a [small list of documented functions](http://wiki.spinout182.com/w/Debug_ROM:_RAM_Map) but that’s by far not all of them.

The way I am currently implementing the gameplay is a big challenge but will give very accurate results and save me a lot of time in the end.