---
title: 'Star Touch'
description: 'Interactive game that teaches constellations.'
layout: project
permalink: /games/star-touch/
---

![StarTouch Header](/assets/images/startouch/header.png)

Star Touch was a project we created for [Dutch Science centre “Nemo”](http://www.e-nemo.nl/en/?id=1). The goal of the project was to create an exhibit that was both fun and educational. The team that created the best exhibit won a free year subscription for Nemo. Which my team won!

### What is Star Touch

When we started we decided that we wanted to do something using the wii mote and the [finger tracking](http://www.youtube.com/watch?v=0awjPUkBXOU) ability. So the idea came to create a game where you had to draw star constallations using your fingers. A constellation showed and blinked for a few seconds then dissapeared and left you with a nice star heaven. The goal was to connect the stars again to recreate the constellation using your fingers as the connect tool. Point one finger at a star and another one at a different star and a line appeared between the stars. When you are done some info about the constellation shows and the top 5 fastest players.

<iframe allowfullscreen="" class="youtube-player youtuber" frameborder="0" mozallowfullscreen="" src="https://www.youtube.com/embed/lb_D2e40x48" type="text/html" webkitallowfullscreen=""></iframe>

### Star Tool

We created a tool to create the constellation files that where needed by the actual program. In the tool you could load a background image and place stars by clicking on the image. Then you could tell it which stars should be connected to form the actual constellation. It saved the files to a custom format which contained the name, description and star positions.

[![StarToolInterface](/assets/images/startouch/startool.png "startool")](/assets/images/startouch/startool.png)

### Used techniques

- Java
- WiiMote library
- BlueCove library