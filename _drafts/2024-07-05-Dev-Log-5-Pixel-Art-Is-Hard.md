---
layout: post
title: Dev Log 5 - Pixel Art is Hard, Use Vectors Instead
author: Richard James
imageurl: /assets/images/dev-log-5/alien.png
---

When you set out to make a new game, it seems like the easy choice would be to utilise pixel art for your graphics. It makes sense that with a limited palette and a limited number of pixels it would be easier to make simpler game characters and environments than trying to work with more complex tools. However, this couldn't be further from the truth.

In my last dev log I talked about my desire to build a game containing entirely original art, built from pixel art in Aseprite. The good news, is that I did manage to build a game from scratch containing completely original artwork. The other good news is that I didn't do it with pixel art!

Here is a screenshot of my game building on previous platformers I have put together. The game is made entirely from original creations, which are all completely animated (idle, run, jump etc.) and this was all made possible by embracing a vector and bone based approach.

<img src="/assets/images/dev-log-5/screenshot.png" class="img-fluid rounded mx-auto d-block px-5" />

I'll talk a little more about my workflow for creating art in a future post, but for now I wanted to cover a few reasons why, despite what trends may suggest, pixel art may not be the way to go for you and your games.

## Limited Pixels

Initially, having a limited number of pixels appealed to me. I figured with only a small number of choices, that I couldn't go far wrong. There are only so many ways to draw a face, or a pair of legs when you are working with only 1,000 pixels. The flipside to this, is that unless you choose those pixels very exactly, your artwork can look wrong, or not work at all! Be prepared to spend a lot of time working out how to translate your relatively free flowing idea into a strict grid.

Big problems that I ran into included drawing legs which looked separate, but not too far apart and fitting all of the facial features onto a character in a way that worked (acknowledging that not all features have to be there with a limited grid size). When grappling with these problems it no longer feels like a fun activity to be creative and produce new art, it becomes a huge problem solving exercise which feels unncessary.

When working with much higher resolutions (such as 4k) or when working with vectors, not having to worry about the imperfections in an individual pixel became incredibly freeing. I can keep my drawings simple, but also have a huge flexibility in the styles and approaches available to me. With my alien drawing below, I had no concerns about the technicalities of drawing my legs, I was free to pursue the style that I wanted.

<img src="/assets/images/dev-log-5/alien.png" class="img-fluid rounded mx-auto d-block px-5" />

## Animation

The problems with limited pixels only become more of a pain when it comes to animation. There are plenty of skills to learn as a solo game developer (art, programming, level design etc.) that I don't have a lot of time to also learn to become proficient in frame by frame animation. I find this to be very time consuming and difficult with pixel art. Posing your characters in the right way with the limited number of pixels becomes a further problem.

With a vector or raster based image approach, it becomes much easier to utilise 2D bone animation such as that found natively in Unity or in a program like Spine 2D. This allows you to take a single image, broken down into parts (such as limbs) and make animations based on the positions of those parts. This removes the need to redraw the character in lots of positions. 

With bone based animations, Unity is also able to smoothly transition between animations, making your game look more slick!