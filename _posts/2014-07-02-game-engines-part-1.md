---
layout: post
category: technical
tags: [javascript, games]
---

I have a tendency to generalize code and often get carried away. On occasion I get right and come up with a nifty set of clean, extensible, generalized code. This is one of those occasions.

## Background

After creating [ShapeEscape](/ShapeEscape) I realized I needed to take a very different direction in game design. ShapeEscape had some unique game play, but overall it wasn't intuitive and didn't have much of a learning curve. Small games should be simple, addictive, and easy to jump into. My goal for my next game was to get all three of these.

Out of the smoldering ruins of ShapeEscape came [Circles](/Circles). The goal of the game is much simpler (click and don't get hit) and there is more variety throughout the levels. It was this variety that I generalized into the game engine.

## Problem

Initially Circles had fairly hard coded levels. There was flexibility on the number of circles and their speed, but that was about it. Let's take a look at some of the code. The Gist below is take almost verbatim from [this commit](https://github.com/TheConnMan/Circles/blob/b2266f5e55616811114e5ea2f55b9443848acb27/js/circles.js).

{% gist TheConnMan/66d904156ddf8a0d3ac7 HardCoded.js %}

Not the greatest, right? When you put these two chunks of code next to each other it's fairly easy to see where some generalization could take place. A lot of rendering using D3 goes on around this code, but these are the guts of the `redraw()` method. Essentially `redraw()` says take the old position (stored in the `d` variable), check if the circle is bouncing off the edge (lines 16-24), and update the position accordingly (lines 26-27). Not terribly exciting.

#### So what do we do?

The improvements we need are twofold. First, we need to generalize the behavior serialization of lines 4-8. Right now the size, speed, radius, etc are a *little* random, but we can do a lot better. What about a changing radius size? Variable speed? Starting angle? Even different physics?

Once we are able to serialize behaviors we need a way to execute them. This will come from generalizing the `redraw()` function. Essentially we'll have to check to see if a variable is a function (i.e. a variable speed) and execute it if it is. This generalized renderer paired with standardized serializations of behaviors is what will become our game engine. Check the next post to see how these generalizations were implemented.

**NOTE:** All code examples used in the posts in this series can be found in a [gist](https://gist.github.com/TheConnMan/66d904156ddf8a0d3ac7) found on [my GitHub account](https://github.com/TheConnMan).
