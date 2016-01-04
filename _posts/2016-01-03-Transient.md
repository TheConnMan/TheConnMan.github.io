---
layout: post
title: "Transient - A Simple Non-Persistent Chat App"
image: http://theconnman.com/assets/images/Transient.png
category: technical
tags: [development, node.js, websockets]
---

![Transient Screenshot](/assets/images/Transient.png)

One of the items on my "To Learn" list recently was [WebSockets](https://en.wikipedia.org/wiki/WebSocket). WebSockets are another of the next-generation (at least five years ago when it was standardized) web technologies which make using websites even nicer for users. From Wikipedia:

> WebSocket is a protocol providing full-duplex communication channels over a single TCP connection.

This means messages can be broadcast to connected clients near instantaneously, so no AJAX polling and no page refresh.

My first experience with WebSockets was when I built a small trivia game which required all connected sessions to show and hide the trivia question simultaneous. That experience was tarnished by extensive use of Internet Explorer 8 and 9 by many of the users (older versions of IE don't support WebSockets and attempt to fall back to polling, often with poor results), so I hoped this experince would be a little better (and a little less "Enterprise"). I figured I'd try building the same thing everyone else seems to use WebSockets for: a chat app.

**NOTE:** The full repo of the following project can be found at [https://github.com/TheConnMan/Transient](https://github.com/TheConnMan/Transient)

## Functionality
The basic functionality is simple:

- Set a username
- Receive all messages to the chatroom after that point
- That's it

Because users can't see messages from before they join the room there doesn't need to be any persistence of messages (aka no database).

I ended up adding the concept of multiple rooms meaning users can join different rooms and only see the messages sent in that room.

A working demo can be found at [projects.theconnman.com:8080](projects.theconnman.com:8080).

Now that we know the very basic functionality, let's take a look at how it was built.

## Toolstack
[Node.js](https://nodejs.org/en/) has very good WebSocket integration and many of the apps I have seen using WebSockets use Node.js, so it seemed like a good choice. [Express](http://expressjs.com/) is a very simple web server which I used to serve up the small [AngularJS](angularjs.org) app. [Socket.io](http://socket.io/) was used to manage the WebSocket connections. I then used [Semantic UI](semantic-ui.com) as my CSS framework. As I mentioned in [Frontend Development for Full Stack Devs](/philosophy/2015/12/20/Frontend-Development.html) my toolstack has recently shifted to use many of the latest-and-greatest frontend dev tools. I have to make sure I don't jump on the bandwagon too much...

## Building Transient
The resulting code for the initial version of **Transient** (which can be found on [GitHub](https://github.com/TheConnMan/Transient)) is somewhat underwhelming. The use of Socket.io and [angular-socket-io](https://github.com/btford/angular-socket-io) made the WebSocket connections extremely easy to manage.

### Express App
The Express app's main responsibility is to receive and broadcast messages. This functionality is shown below in an excerpt from the Express app (**app.js**) and a helper class (**rooms.js**).

{% gist TheConnMan/40b9c918a91b074adf51 app.js %}

The code above shows just how simple the WebSocket connections are. After a connection is made five commands are registered with callback functions.

One benefit of WebSockets (and reason for refactoring halfway through the project's initial build) is that socket connections can persist user data within them. This allows the Express server to store a session's username and current room so that data doesn't need to be sent with each message. This has serious security implications which I won't go into here.

{% gist TheConnMan/40b9c918a91b074adf51 rooms.js %}

Above is the helper code used to make the Express socket callbacks a little cleaner. There isn't much to it other than a few more socket commands. The `rooms.send` function takes care of all broadcasting to connected clients. All broadcast messages are small JSON payloads to be rendered by the Angular app.

### Angular App
The WebSockets parts of the Angular app are even simpler than the server. In the Gist below I ignore all the Angular routing and view updates and only show the code responsible for sending and receiving messages.

{% gist TheConnMan/40b9c918a91b074adf51 public-js-app.js %}

The Angular plugin lets the app make a similar `socket.on` call to register message callbacks and then can emit messages with `socket.emit` as well.

### Docs and Docker
Normally after the actual app is built I would just leave it as-is. Recently I've been trying to make an effort to make sure all software I build, including small side projects, have all the appropriate documentation to be run by someone else. This is as much to get in a good habit as it is to help others run my open source software (if that day should ever come...).

Conveniently, writing install docs for Node (especially when using Docker) is extremely easy. A Dockerfile and install docs are both included in the repo.

## Conclusion
The **Transient** app is, as promised, very simple both in functionality and construction. It was a fun project to build (I ended up spending more time on it than anticipated) and it provided a good experience into WebSockets. Unfortunately, I found out afterwards that pretty much everyone has made a simple non-persistent chat app, so I didn't make anything unique. Regardless, I learned some things and have yet another project to cannibalize for future projects.
