---
layout: post
category: technical
tags: [javascript, games]
---

# Recap

In my [last article]({% post_url 2014-07-03-game-engines-part-2 %}) I discussed how we could serialize different behaviors by storing functions within data objects. This article will finish up my game engine trilogy by talking through the underwhelming amount of code needed to render these serialized functions.

# The Grand Finale

The last piece of the puzzle is to create an engine to evaluate the serialized behaviors we developed in the last article. If we were smart in our conventions earlier then the heavy lifting should be over. The code below if the finalized game engine and the amount of code may be a little underwhelming (most of it is comments).

{% gist TheConnMan/66d904156ddf8a0d3ac7 Engine.js %}

The fact that the total amount of code used to define each circle and re-render them can be compressed to under 40 lines is a very good thing. This means that we've done such a good job in our definitions that we don't need to waste code catching corner cases, enabling additional functionality, or looking for exceptions. The engine could easily be 5x as long if the code had been *added to* instead of *refactored*. I can imagine myself writing this game a year ago and seeing if statements all over the place. Let's take a look at each component of the code.

## Definitions

Below is a comparison of the new and old definitions section.

{% gist TheConnMan/66d904156ddf8a0d3ac7 CompareDefinitions.js %}

The general structure of both definitions doesn't look terribly different. We still define each circle's data inside a single object, there's just a bit more of it. Notice that we only check to see if one element is a function: starting angle (line 37). It would have been very easy to put a lot of if statements in this section to check if elements are functions or not and deal with them accordingly. Instead, we pass them through and deal with them inside the `redraw()` function.

## Engine

Below is a comparison of the new and old re-render section.

{% gist TheConnMan/66d904156ddf8a0d3ac7 CompareEngine.js %}

Again, at first glance both `redraw()` functions look very similar and again this is good news. Some smart refactoring occurred to preserve the same structure (the nature of the game wasn't changing) but make it more flexible. Circles still move, but *how* they move can change. Let's take a closer look how each circle can change in a single refresh:

- Radius (lines 28 and 55)
- Momentum* (line 30)
- Position (lines 46 and 47)
- Position when reaching a boundary (lines 36 and 42)
- Trajectory angle when reaching a boundary (lines 37 and 43)
- Angle during a random angle change (lines 49-52)

When you list out what can change on a single redraw, it really isn't that much. It can basically be summed up by "where it is" and "where it's going". The true flexibility comes from how these changes are evaluated. A recurring theme in the code above is `physics.[function](arguments)`. Instead of predefining behavior, the engine acts and a glorified function caller. How far does the circle move? However far `physics.xx()` and  `physics.yy()` say. What is the new radius? Whatever `d.radius` evaluates to.

\* I chose to change **velocity** to **momentum**. To convert momentum into velocity I divide the momentum by the current radius squared. I wanted the physics to be more realistic in that way...until I had momentum change too.

# Conclusions

It seems a little like cheating because there really isn't any magic happening. All we're doing is abstracting out a few standard functions and evaluating they each time the viewport is refreshed. The heavy lift was figuring out which functions we could abstract and essentially creating an internal API for ourselves. Even as I write this I'm thinking "Why can the trajectory angle only change at a boundary?" and "Why can't the circle color change?" Theoretically *every* aspect of a circle (rectangle? polygon?) can change on `redraw()`, it's just a matter of what is supported.

## My Experience

I had a great time creating Circles. It was a new type of project for me and I learned quite a bit about how to structure projects. The amount of code wasn't overwhelming, but the complexity was a challenge to wrap my head around. As I said before, I could have written Circles a lot faster with a lot more code, but I wanted to spend the time to do it right. After many, many refactorings I got it to the stable place it is now. I haven't worked on it much lately, but expanded on the game engine idea with [ShapeEscape](/ShapeEscape) (especially the physics part). I hope to write a post about that expansion at some point, but these three posts have been a lot of writing this weekend.

Thanks for reading, I got to get back to coding.

TheConnMan

**NOTE:** All code examples used in the posts in this series can be found in a [gist](https://gist.github.com/TheConnMan/66d904156ddf8a0d3ac7) found on [my GitHub account](https://github.com/TheConnMan).
