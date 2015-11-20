# Chapter 5 - Solid Chess

![](https://melvincarvalho.gitbooks.io/solid-tutorials/content/solidchess.png)

## Introduction

In this tutorial we will cover how to play a game of chess in reatlime using Solid and websocket updates.  A JavaScript board is embedded in the page, updates occur in realtime, and a link is provided to a chess engine to enable hints.

*What you will learn*

* How to add websocket support
* How to send moves to a Pod in realtime
* How to update the board when a new move is made remotely
* How to create your own vocabulary
* How to embed a JavaScript chess widget in a page
* How to link to a chess engine for hints

## The App

The main aspect of this tutorial is realtime updates via websockets.  Solid uses a pub/sub mechanism to allow users to subscribe to a resource, and will send pub updates when one of those resources changes.

Websockets are built into the browser and are started using the 

```JavaScript
    new WebSocket()
``` 
    
syntax.  



More Coming soon ...


## See Also

* [Source Code](https://github.com/melvincarvalho/chess)
* [Live Demo](http://melvincarvalho.github.io/chess/)
