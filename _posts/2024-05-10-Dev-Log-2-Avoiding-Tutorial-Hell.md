---
layout: post
title: Dev Log 2 - Avoiding Tutorial Hell
author: Richard James
imageurl: /assets/images/dev-log-2/cover.webp
---

Something I am keen to avoid, is getting stuck in a "Tutorial Hell". This is a state where you follow lots and lots of tutorials online, but you get stuck never really being able to create something on your own. With that in mind I have spent my week prototyping and exploring a few new ideas.

I have an idea for a game in my head which takes a little bit of inspiration from Theme Hospital. One of the key concepts in the game is that agents visit a number of locations based on needs which change over time, and that those agents may have to queue for a particular location if others have beaten them there.

With that in mind I set out this week to build a prototype game with at least some of those features. However, there were a few things I wanted to try out first.

## Arena Battle

The aim with this game was to build a small fighting game with the following features

1. Enemies which moved to your location.
2. Basic fighting mechanisms (swinging a sword to hit enemies and deal damage)
3. A secondary attack (magic)
4. Some basic fighting mechanics such as knock back, hit points and enemy states (they run away when hit)

These are all of the features I intended to build. In fact, keeping the scope controlled is key to progress. I haven't built features which some would consider obvious (the player can't be hurt) because the wouldn't teach me anything. I'm not aiming to build a game - just to practice.

<img src="/assets/images/dev-log-2/arenabattle.png" class="img-fluid rounded mx-auto d-block px-5" />

It's not much to look at, but I managed to implement hit boxes and hurt boxes, a de-coupled way for those components to talk to each other, and a state machine for the enemies.
I also implemented mouse controls for the sword and a particle effect (which doesn't look great!) for the magic which I wasn't expecting to pick up.
There is still more to learn - the AI pathfinding is very basic, but I got what I needed.
[You can play this game here](https://tangerine-sorbet-a199e8.netlify.app/)!

## 3D Dungeon

The next project was a small 3D dungeon game. The aim with this project was to start working in 3D. This involved importing pre-built assets (from KayKit) and building an environment. I also utilised the GridMap system and implemented a full set of camera and movement controls which mimic most 3rd person games.

<img src="/assets/images/dev-log-2/3ddungeon.png" class="img-fluid rounded mx-auto d-block px-5" />

Again - the features are kept pretty minimal. You can attack the skeletons and both they and the player have states to help manage this. However, the main thing was just to cover the small pieces I need to move to the next game with a few more concepts and patterns under my belt.
[You can play this game here](https://resilient-pastelito-6f65dd.netlify.app/)!

## Food Court Tycoon

The last project for the week was the beginning of what will hopefully become a "proper" game. At the same time it proves out some of my thoughts around a queueing system and introduced me to some more concepts around projection (orthagonal vs perspective), agent simulation and NavMesh navigation.

<img src="/assets/images/dev-log-2/foodcourttycoon.png" class="img-fluid rounded mx-auto d-block px-5" />

On top of that I also picked up Blender after a long hiatus and built some very simple models for the customers, for the stalls, for the trees and for the tables. These were just very quickly put together, but I plan to spend some more time building my own assets to have some original artwork to work with.
I'm not very good at 2D work, so the move to 3D was an important step for me!
I'll talk about this much more in a future Dev Log. [For now you can play the beginnings of this game here](https://cosmic-croissant-0da9eb.netlify.app/)!
