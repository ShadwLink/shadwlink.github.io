---
title: 'Shadow-Mapper lives (sort of)'
date: '2022-09-07T20:00:00+02:00'
author: Shadow-Link
layout: post
permalink: /shadow-mapper-lives/
categories:
    - Games
tags:
    - gta
    - modding
    - tools
---

After 13+ years I got curious to see if Shadow-Mapper would still build and run.
Checked out the [git repository](https://github.com/ShadwLink/Shadow-Mapper) and it was immediatly clear that it would not build let alone run.

So I decided to take up the challenge and see if I could make it run or at least build after all those years.

**Step 1 - Replace build system**
The old version of Shadow-Mapper was build using netbeans and used the netbeans project files and way of building.
I've decided to use Gradle as a build/dependency management system. Gradle is supported by many Java IDE's and has great support in Intellij.
After settings up the Gradle build file the project could still not build.

**Step 2 - Find missing dependencies**
The project was still missing a lot of dependencies which where previously added to the classpath by the Netbeans project.
Tracking down those missing dependencies was easy; Just search for the package on Google and in most cases the libs where available on MavenCentral.

**Step 3 - Actually getting the project to work**
As the project is really old and was one of my first "big" projects, the code is terrible to say the least.
I've had a few good laughs at the codebase but most of the time it made me sad (Might be worth a post on it's own), it's insane that this actually worked!

Some interesting changes that where required:
- GTA: IV has been updated so fetching the encryption key from the game needed an update.
- A lot of resources could not be loaded due to broken file parsing.
- The OpenGL canvas was only drawn once.

After a lot of minor changes the project is running again, without textures mind you.

This is the current status for now, not sure if I will spend more time on it, but at least everyone checking out the [repository](https://github.com/ShadwLink/Shadow-Mapper) should be able to build the project!