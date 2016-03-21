---
layout: post
title: "Development Black Boxes"
category: philosophy
tags : [philosophy, development]
---

I've recently moved from primarily developing in the realm of [Grails](https://grails.org/) to one level deeper with just [Spring](https://spring.io/). Both are Java frameworks and Grails is built on Spring (Grails 3 recently being built on the popular [Spring Boot](http://projects.spring.io/spring-boot/)). Taking a step down into Spring has started to open my eyes to some of the "black magic" that Grails takes care of for you. Even Spring Boot is a very [opinionated framework](http://stackoverflow.com/a/802064). These opinions (aka defaults) can be black magic if you don't know what they are when you dive in. This has lead me to the question: How much black magic is too much and is this just the new development world we live in?

# Black Boxes
I may be being a little too harsh when I label these defaults and frameworks as black magic. By definition anything a developer uses which they didn't write (or wrote and have since forgotten) is a black box to a certain degree. There are lots of ways to compartmentalize services (that's what [Object Oriented Programming](https://en.wikipedia.org/wiki/Object-oriented_programming) is all about, right?), but these frameworks and projects take that to a whole new level. The example I like to give is the following scenario:

> Imagine you are running a Grails application locally (no need to delve into infrastructure issues...). You go to refresh a page and you are presented with a 500 error. Where's the problem? Is it a GSP (Groovy Server Page) rendering error? What about a Grails controller issue? Illegal [Groovy](http://www.groovy-lang.org/) syntax? Maybe a [GORM](https://grails.github.io/grails-doc/latest/guide/GORM.html) (Grails Object Relational Mapping) issue? [Hibernate](http://hibernate.org/)? The [MySQL](https://www.mysql.com/) DB you're using? How many of these technologies are really black boxes to you?

The scenario above has happened to me so often that I consider it the norm. Thankfully, I went into developing Grails apps with a little MySQL and Java experience. But still, someone learning everything in the above scenario will have a hard time figuring out where the boundaries are between the technologies. This is exactly what I'm finding out by taking a step back into Spring. I'm now discovering how much of Grails was because of Grails and how much was from Spring. It's giving me a better understanding of both frameworks.

Full stack developers are more users and integrators of frameworks than developers of a particular set of languages. Yes, there's basic syntax to follow (or is there really with [CoffeeScript](http://coffeescript.org/), [Groovy](http://www.groovy-lang.org/), and [Babel](https://babeljs.io/)?), but most of the rules we follow and use are conventions created by the particular framework. Even [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) is a construct of these frameworks, just another way of organizing conventional code. I'm sure I'd be hard-pressed to write straight Java that really did anything of significance.

# The Third Age of Development Languages
This is, however, the natural progression of things. You don't see anyone (ok, maybe _many_ people) building their own OS's anymore. New development languages don't come out very often. Most of what I see on GitHub is new frameworks. Just search for "mvc framework [insert language here]" and I'm sure you'll find many results. This isn't even getting into the proliferation of JavaScript everything that is happening these days. We're in what I believe to be the third generation of application development languages.

1. **Bare Metal** _[C, Assembly]_ - These are the early development languages which interacted directly with the moving parts of a computer. If something went wrong you could probably trace the issue all the way back to the true source and have full control over everything in-between.
1. **Object Oriented** _[Java, .NET, JavaScript]_ - These are some of the largest first-level abstractions away from bare metal. The [JVM](https://en.wikipedia.org/wiki/Java_virtual_machine) is a very interesting abstraction which allows developers to interact with it on a higher level than they would be able to interact with the host machine.
1. **Frameworks** _[Grails, Node.js, ASP.NET MVC, Spring]_ - These are the next level of abstraction away from the base languages. Frameworks are not a new concept, but they have really taken off in the last decade. Much of what end developers interact with are the conventions put in place by the framework(s) they use, not just the syntax requirements of the underlying language.

# The New Development Landscape
I believe that the ability to pick up new languages and frameworks is important now more than ever. Debugging simple issues has become trivial with the internet and anything basic in an application has already been done many times by someone else. We are continually building on the shoulders of giants and being able to look all the way down to the ground and debug is extremely valuable. Much of what we debug day-to-day is not actually our own code, instead debugging our own misuse of someone else's.

Black magic and black boxes are definitely here to stay. I continue to strive to be as good of a generalist as I can so that I can jump in and help wherever I can. I think even the definition of a specialist is changing. I doubt anyone truly only works in one language anymore. Everyone has had to write a little Bash, tweaked some CSS, or debugged some JavaScript. All of these languages and frameworks are some intertwined that it's hard _not_ to use multiple languages. Most of us don't even notice, it's just part of the job. The key is to know how much you need to know about a language or framework to build on top of it: too much and you don't have enough time to move fast, too little and you become irresponsible and create more work for yourself down the line. For each person it is a different balance.