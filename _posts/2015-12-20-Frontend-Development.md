---
layout: post
title: "Frontend Development for Full Stack Devs"
category: philosophy
tags : [philosophy, development]
---

A few months back I went to the SpringOne 2GX conference to learn about the latest and greatest for Spring and Grails. The talks I focused on were mainly on server-side Grails and system architectures (like **microservices**, which I've been [playing around with](https://github.com/TheConnMan/microservices) quite a bit lately). The last talk I attended, however, was called [Modern Frontend Engineering](https://2015.event.springone2gx.com/schedule/sessions/modern_frontend_engineering.html) and focused on frontend development. I consider myself a full-stack dev, so frontend development is just part of the job. I went into the talk expecting to learn a few things, but instead I got a wakeup call.

The talk, which has slides [here](http://www.slideshare.net/SpringCentral/modern-frontend-engineering) dove into everything from frontend dependency management ([Bower](http://bower.io/)) and task running ([Gulp](http://gulpjs.com/) and [Grunt](http://gruntjs.com/)) to CSS frameworks ([Bootstrap](http://getbootstrap.com/) and [Semantic UI](http://semantic-ui.com/)) and MVC frameworks ([AngularJS](https://angularjs.org/), [Ember](http://emberjs.com/), and a dozen others). This doesn't even begin to consider everyone is using [Node](https://nodejs.org/) to run all of the above tools and to serve up their [single-page applications](https://en.wikipedia.org/wiki/Single-page_application). Apparently nobody writes heavy, coupled web applications anymore.

**That was news to me.**

I'll admit I came out of that talk a bit scared. I thought that if I just found enough cool tools and put in a few hours outside of work to focus on frontend development and that "User Experience" thing I'd be OK. That talk was a wakeup call that I can't truly compete with frontend devs as a full-stack dev. It might have been at one point, but those days are definitely over.

## Reaching Acceptance
Since the conference in September I've had to come to terms with a few things:

- The apps I build frontends for will not have the quality, flexibility, or customization of frontends built by frontend devs
- I need to find tools and frameworks to augment my own development ability, as much as I might like to build from scratch
- I will need to live with the "out of the box" functionality of those frameworks
- Most of my apps will look the same
- **I will never be on the cutting edge of frontend development**

That last one can be generalized to:

> As a full-stack dev, I will never be on the cutting edge of anything

That's a bit grim (and a bit of an exaggeration), but I'm beginning to believe it's more true than not. **There is too much ground to cover today and being a full-stack dev means not being an expert in anything.**

## Toolstack Overhaul

### The Old Stack
Over the past couple months I've taken a hard look at my toolstack. It generally was:

- Grails, jQuery, and Semantic UI for web apps
- Python or Groovy for small utility scripts
- Bash or Python for command line utilities
- Crossed fingers for containerization

The stack above is, besides a little old-fashioned, not scaleable. It's great for smaller apps and scripts, but those are fewer and further between. It's also very manual. Web app frontends become a mess very quickly when everything is wired with jQuery.

### The New Stack
Now compare the above with my new stack below:

- Grails or Express, AngularJS, and Semantic UI for web apps
- Node.js for small utility scripts
- Node.js for command line utilities
- Docker and Vagrant for containerization

You could say I've jumped on the bandwagon.

The move to learn AngularJS was caused by many reasons, but one big one was the announcement that [Grails 3.1 would have an AngularJS profile](http://grails.github.io/grails-doc/3.1.x/guide/introduction.html#webApiAndAngularProfiles). Learning AngularJS has been great so far, especially when [AngularJS Resources](https://docs.angularjs.org/api/ngResource/service/$resource) is combined with [Grails REST Web Services](http://grails.github.io/grails-doc/latest/guide/webServices.html). Those alone have saved me a ton of time writing CRUD functions for REST services.

And if you're going to learn anything like Bower or AngularJS you'll have to learn Node.js. One thing lead to another and I've started using Node.js for just about everything.

Finally, Docker has been a necessity for a few projects and it works really well with the above tools (though I would have learned it just for the amount of time it's saved me when trying to run other people's projects).

## Conclusion
The moral of this story is that these days in web development you do have to specialize, even if that specialty is being good, but not great in everything. I've only got so much time, so I look for the minimum tool stack that can do the most for me so I'm not spending all my time keeping up with the updates to my stack. I've also come to terms with not making the most beautiful, most interactive applications by myself, there just isn't time for it all.

There's a lot of great frontend devs out there making a lot better stuff than I can. I can't wait to start using it on my apps.
