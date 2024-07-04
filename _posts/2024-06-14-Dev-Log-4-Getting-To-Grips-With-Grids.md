---
layout: post
title: Dev Log 4 - Getting to Grips with Grids
author: Richard James
imageurl: /assets/images/dev-log-4/pixelart.png
---

There have been a few updates since my last post here. The first being that I spent a little money to upgrade my computer. I had previously been using a Core i5 4670k with 8Gb RAM and an NVidia GTX 1060 3Gb. That’s a 10 year old processor, with a pretty weak graphics card. It’s served me well for a long time, but I am way overdue an upgrade.

Anyway — for a few hundred pounds spent on eBay I am now sporting a Ryzen 5 5600, 32Gb RAM and an NVidia GTX 2060 Super. This is still not a powerful machine, but works great for 1080p gaming and has made a huge difference in the performance of some applications.

The main application it has made a difference with being Unity.

In my first Dev Log I talked about choosing between Unity and Godot, and despite preferring the technology and workflow of Unity, picking up Godot because of performance issues. Those issues are now gone, and I have been able to use Unity much more easily and quickly.

A lot of games use a grid based system and mechanics for building and I wanted to spend some time to get to grips with those sort of systems. I started with a few YouTube videos which worked on the basis of using a number of Prefabs to represent each square in a grid, and then building a dictionary of these squares with vectors to represent the position.

This seems to be a pretty common approach on YouTube, but I am guessing that none of them tried a grid of any size. This approach works great with a hundred or so tiles (say, a 10x10 grid) but performance is absolutely tanked once you get much beyond that due to the number of sprite renderers and other components.

Other than this though, the approach most took was fairly sensible and I was able to adapt it to use the built in Unity TileMap features, holding the state of my grid in a dictionary of scriptable objects (representing each tile) and then using the TileMap to reflect that into the UI.

Following on from my previous fast food truck idea. I build a small prototype which allows you to build paths and shops, and to spawn in customers who can navigate the map based on whether each tile is “walkable” or not. This short YouTube video shows the finished results.

<style>.embed-container { position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; } .embed-container iframe, .embed-container object, .embed-container embed { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }</style><div class='embed-container mb-3'><iframe src='https://www.youtube.com/embed//a_ex1MhpIns' frameborder='0' allowfullscreen></iframe></div>

I’m quite pleased with the results, and alongside remaking a platformer in Unity it allowed me to get to grips with the main features and match my skill level back to where I had reached with Godot.

The other skill I have been trying to hone is my game art. In particular a 2D pixel art style. Working with a mouse alone was not doing much for me here, and so I have bought a drawing tablet and started practicing. So far my results are mixed (the example below is the one I am most proud of) but I feel that this is the area that will make or break my game making.

<img src="/assets/images/dev-log-4/pixelart.png" class="img-fluid rounded mx-auto d-block px-5" />

I’ve spent a long time in my life and career studying programming and technology, and those skills come easily to me. Art is a different beast. Although I believe anyone can learn a skill with enough time, I think this will be the challenge for me, and is the main focus of my skill development for my next game — a platformer (because I’ve done that before) featuring completely original artwork!

Keep watching this space!
