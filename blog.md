---
layout: page
title: Welcome
tagline: An Introduction
---
{% include JB/setup %}

This is a blog for mainly JavaScript things, but topics vary.

## About Me

I'm a software developer who has a recent interest in web development. I'm an MIT grad with a Physics degree, so I'm going back to my roots by writing some game engines (not really, I haven't implemented any Quantum Mechanics). Before web development I've mainly worked with Java and Python. Web development seems much more interesting.
    
## Posts

Here are the most recent posts:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

