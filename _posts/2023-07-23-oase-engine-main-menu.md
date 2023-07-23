---
title: 'Main menu in OASE engine'
date: '2023-07-23T12:50:00+02:00'
author: Shadow-Link
layout: post
permalink: /oase-engine-main-menu/
categories:
    - Games
tags:
    - oase
    - game
    - engine
    - gta
    - vc
---

After taking a break from [OASE](https://www.youtube.com/playlist?list=PLOxyV5A-M9P38WibzT8wnz0Teq9oMzqbU) (did I ever mention this project before?) to work on some other side projects, I wanted to work on it a bit. 

Last time I worked on the engine the MacOS version had some depth rendering issues, so I decided to dive into the issue and fixed it pretty quickly. With the issue sorted out I decided it was time to do a bit of work on the main menu. Playing around with the stencil buffer to implement the dynamic background gave me the following result:

![OASE Main Menu](/assets/images/engine/main_menu.png)

Not only the look of the menu is starting to look like the real deal, thanks to the great documentation on [gtamods.com](https://gtamods.com/wiki/Gta_vc.set), I was also able to implement loading and saving of the gta_vc.set file and actually use the values stored in the file for the draw distance and language.

That's it for now, I might post a bit more info about the OASE engine and the progress I've been making in the future.
