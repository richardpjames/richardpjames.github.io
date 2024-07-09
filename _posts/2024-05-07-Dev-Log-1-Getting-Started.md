---
layout: post
title: Dev Log 1 - Getting Started
author: Richard James
imageurl: /assets/images/dev-log-1/cover.webp
---

For some time, I have wanted to create my own game. It fits really nicely with a few hobbies that I already have (programming, music and art) and would scratch a creative itch.

I have no intention of making any money from my games (I already work full time in the software industry) so it’s all about fun for me. As such, I want it to be a relatively pain-free experience, but I also don’t need to worry about any commercial aspects either.

I don’t want to do everything from scratch — I want to get right into creating a game. The best approach to do this is to pick up a game engine.

There are a number of engines available for creating games, but the main players are:

* Godot
* Unity
* Unreal
* GameMaker

Each provide a full set of tools and have been used to create successful games, so which is best (or at least best for me)?

<img src="/assets/images/dev-log-1/godoteditor.png" class="img-fluid rounded mx-auto d-block px-5 px-5" />

An initial review of the features and focus of the engines led me to look at Godot and Unity. I decided to download both and try to create roughly the same game with each. For no particular reason, I decided to start with Godot.

At this point — I have no idea how to create a game, so I decided to look around for some tutorials. I signed up to [Udemy](https://www.udemy.com/) (who offer a free seven day trial on their subscription services). I then started the [Jumpstart to 2D Game Development: Godot 4 for Beginners](https://www.udemy.com/course/jumpstart-to-2d-game-development-godot-4-for-beginners/) course.

To start with — things were going well and I felt like I was picking up the basics. However, there were a couple of problems:

* The course is over 38 hours long, which is a big commitment to picking up the basics
* My previous experience means that I don’t need the basics (programming syntax etc.) explaining, I just need to know how to use the engine to make something simple

So — I gave up on this approach after watching the first set of lectures on creating Flappy Bird.

A quick scan of [/r/godot](https://www.reddit.com/r/godot/) showed that I just happened to start out at the same time a popular Unity YouTuber (Brackeys) was creating new tutorials for Godot. At just over an hour long, this seemed perfect. By the end of the video I would have a working game and a good jumping off point.

To me, this approach was perfect, and you can [view the video on YouTube](https://www.youtube.com/watch?v=LOhfqjmasi0)! If you follow along you’ll end up with something like the picture below!

<img src="/assets/images/dev-log-1/platformerrunning.png" class="img-fluid rounded mx-auto d-block px-5" />

After finishing the tutorial I went ahead and tried to extend the game a little, adding a double jump and end game state. I also re-factored some of my code using some techniques I had learned from the Udemy course (perhaps it wasn’t a waste of time completely!).

<img src="/assets/images/dev-log-1/unitysplash.png" class="img-fluid rounded mx-auto d-block px-5" />

Next I wanted to try and build the same game again in Unity. I looked for another basic tutorial (this time following [The Unity Tutorial for Complete Beginners](https://www.youtube.com/watch?v=XtQMytORBmM) by [Game Maker’s Toolkit](https://www.youtube.com/@GMTK)). The good news is that a lot of the same concepts follow over from one engine to the next, but their implementation is just a little different.

With just a couple of hours worth of tutorials I was able to create roughly the same game in both engines (I didn’t complete the Unity version as I had got far enough to understand the differences in approach).

<img src="/assets/images/dev-log-1/unityeditor.png" class="img-fluid rounded mx-auto d-block px-5" />

To start with, I thought that Unity had a lot going for it. I quite liked the pattern with prefabs, a few of the tools felt a bit more polished and I liked working with Visual Studio Code and C# for building the game (I know that you can use C# with Godot as well).

Unity is getting a lot of heat from other game developers online due to a recent change in their commercial model, but this doesn’t really bother me (I’m not planning to make any money just yet).

However, having actually used the engine for a few hours, there seemed to be some things which were just easier or better in Godot. I don’t mind if there is a single use case which is a bit trickier in one engine (each engine will have strengths and weaknesses), but this seemed like a pattern.

* The built in CharacterBody2D in Godot allowed for easily detecting whether a character was on the floor or hitting a wall. Lots of Googling revealed different approaches for this in Unity, but they all required more work.
* Inputs seemed much easier to deal with in Godot and I wasn’t required to install additional packages to use the tools.
* GDScript (Godot’s built in language) is actually really nice! It’s designed specifically to work with the engine. A nice feature is being able to Ctrl+Drag any node into a script and immediately have a variable ready to use. In Unity this involved declaring a variable, and then going back into the engine editor and dragging components around.

…and as well as the three examples above, I just found more places where Unity just didn’t gel with me. My main gripe though, was the performance. Not the performance of the games — but of the editor. It felt like I was always waiting for something to load or download and install.

I decided that (at least for now) Godot with GDScript is the one for me.

<img src="/assets/images/dev-log-1/godoteditor2.png" class="img-fluid rounded mx-auto d-block px-5" />

Am I saying that you should definitely choose Godot for your project as well?

Absolutely not!

There are some definite downsides to Godot as, such as not being able to publish your games to the main home consoles. You may also find that you don’t like the workflow, or the GDScript language. It’s not for everybody.

I think that the main thing I have learned, is the value of small projects and proof of concept exercises. In this example, if you’re unsure which engine you want to use, then try them out (or at least a subset). Don’t listen to the plethora of YouTube videos and internet comments telling you which engine is “best” — find out for yourself (you might be surprised)!

The same will apply throughout the journey — try something small and whether you fail or succeed you can take your learnings forward into your next project. Don’t get stuck in tutorial hell, or watching endless videos. Try and do some things and learn along the way.

As a final note: if you’re interested, you can [play the finished platformed that I (and probably many others) built here](https://brackey.richardpjames.com/)!