---
layout: post
title: "Game Engines Part 2"
tagline: "A Lot Of Refactoring"
category: coding
tags: [javascript, games]
---
{% include JB/setup %}

# Recap

[Last article](/coding/2014/07/02/game-engines-part-1) I laid out the problem of having very restrictive code within my game [Circles](/Circles). This post will describe how to reshape this interior code to intelligently evaluate parameters instead of relying on those parameters to be fixed. We'll also explore a little of the flexibility which falls out of developing this game engine.

##  A Little Generalization

Now that have an idea of what we should do we can make some improvements. Let's work on serializing behaviors first. We'll stick with the notion of embedding data within an array of objects and just tweak it a little. We'll define a `levels` object which contains metadata definitions of each level. A trivial example (level 1) is shown below.

{% gist TheConnMan/66d904156ddf8a0d3ac7 LevelExample1.js %}

By convention the keys of `levels` will be the level numbers and the values will be metadata objects. Lines 2-9 are fairly straightforward and we can see how they would fit into the engine. On level initialization the data for that level will be passed into the renderer as, say, `params`. Instead of a fixed number of circles we'll use `params.ballNum`, instead of a fixed expansion speed we'll use `params.expandSpeed`, and so on. We can even give the level a custom name with `params.title`.

So now the game is a *little* more generalize, but come on, we can do better. Parameterized, yet fixed, values give us the flexibility to define different levels, but once the level has been initialized all behaviors are static. Let's see what else we can do.

## Getting Functional

### A Slight Digression

Recently I read a book on functional programming in JavaScript and found it a bit abstract. I learned programming through a lot of for loops and if statements, so passing functions into other functions which return functions seemed very unnecessary. I had to check the cover a few times to make sure the author wasn't Xzibit. (Ok, I lied, it was a Nook book, it didn't have a cover). Little did I know that I had been using functional programming for the past year.

Over the past year I've learned a lot of Groovy (the lazy sibling who mooches off of Java) and have used a lot of closures. Closures are at their core functions passed into other functions, which is functional programming. A simple example is shown below.

{% gist TheConnMan/66d904156ddf8a0d3ac7 GroovyExample.groovy %}

One of the many great things about Groovy is that it is readable. That one line says:
- Take the array `[1, 2, 3, 4]`
- Square each element
- Sum the elements of the resulting array

For those of you interested in the JavaScript version, it's shown below.

{% gist TheConnMan/66d904156ddf8a0d3ac7 JavaScriptExample.js %}

The JavaScript example is much more explicit in passing functions into other functions. It is very clear that the arguments of the `map()` and `reduce()` functions are functions. Groovy is just a bit more subtle (lazy).

It was this exposure to functional programming which got me thinking about functions in a very different way. What if instead of passing static values into a level we passed functions...?

### Back On Track

Our tangent leads us into the next type of level abstraction shown below.

{% gist TheConnMan/66d904156ddf8a0d3ac7 LevelExample2.js %}

Here we notice a very similar setup to before, but with one striking difference: `expandSpeed` is now a function.

A very reasonable question is "What is `d`?" This is where a strict convention comes in. We need to decide what data will be passed into the parameters during execution so our behavior serialization and game execution line up. For simplicity and flexibility I chose to pass in the entire user circle definition object for functions referencing the expanding circle (e.g. expandSpeed). This object holds the current position, trajectory, momentum, size, etc so it seemed a reasonable parameter to pass in. One component of the circle definition is `o`, a random double between 0 and 1.

Let's take a closer look at the function in lines 8-10. Expand speed is the speed at which the user's circle expands, so setting it to a function means that the speed will fluctuate as it's expanding. This particular example fluctuates between an expand speed of 0 and 2 with a period of 1 sec. Where the expand speed starts between 0 and 2 is random based on the current time (`new Date()`) and a random offset (`d.o`). This is what gives level 23 a little unexpected flavor. This might trip up a user at first, but the game dynamic is more or less the same. What if we *really* wanted to frustrate the user?

### So Close...

I got a lot of complaints about level 24, so I figured I did a good job with it. It's also a good example in feedback loops. Take a look at the code below.

{% gist TheConnMan/66d904156ddf8a0d3ac7 LevelExample3.js %}

As you may know, the expansion speed of level 24 goes down as the size of the circle gets bigger, leading to a log of games where you were "so close". That behavior is reflected in the code where expandSpeed is approximately proportional to how much bigger the circle needs to be to win. My apologies to everyone who quit on this level. My apologies, of course, for not being sorry.

## Gettin' Physical

The last example adds one last kind of tweak to the serialization. In the code below different physics are applied to the circles.

{% gist TheConnMan/66d904156ddf8a0d3ac7 LevelExample4.js %}

The physics defined in lines 2-17 are also stored within an object of functions. These functions will be executed along with the other parameters inside the game engine. The notable differences between `ghostPhysics` and `defaultPhysics` (not shown) are lines 6-13. Lines 7 and 9 make the new x and y positions the old positions plus the change mod the width or height. In non-code speak, if a circle hits a border it flips over to the other side (like a ghost). Because there is no need to reflect the circle's trajectory lines 11 and 13 return the original angle.

## Next

It's amazing how much flexibility can come from just a few abstractions. Pulling out level definitions into a single `level` object helped us define distinct levels, but it was really the leap to setting those metadata definitions to *functions* that brought the flexibility. Once that was in place we could define all sorts of dynamic behaviors. This is only half the battle, though, because now we need to refactor the hard coded `redraw()` function to something that can render these behaviors. Check out the next post to see how we can transform it into a game engine.