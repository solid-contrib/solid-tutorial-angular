# Chapter 5 - Solid Chess

![](https://melvincarvalho.gitbooks.io/solid-tutorials/content/solidchess.png)

## Introduction

In this tutorial we will cover how to play a game of chess in reatlime using Solid and [Websockets](https://en.wikipedia.org/wiki/WebSocket) updates.  A JavaScript board is embedded in the page, updates occur in realtime, and a link is provided to a chess engine to enable hints.

*What you will learn*

* How to add [Websockets](https://en.wikipedia.org/wiki/WebSocket) support
* How to send moves to a Pod in realtime
* How to update the board when a new move is made remotely
* How to create your own vocabulary
* How to embed a JavaScript chess widget in a page
* How to link to a chess engine for hints

## The App

The main aspect of this tutorial is realtime updates via websockets.  Solid uses a pub/sub mechanism to allow users to subscribe to a resource, and will send pub updates when one of those resources changes.

[Websockets](https://en.wikipedia.org/wiki/WebSocket) are built into the browser and are started using the 

```JavaScript
    new WebSocket(uri)
``` 
    
syntax.  After opening the websocket we then have access to the `onopen`, `onclose`, `onerror` and `onmessage` functions.  When a socket closes or errors, we would like to restart it so we will call a restart function.

```JavaScript
    socket.onerror = function(){
      console.log('socket error');
      setTimeout(connect, RECONNECT);
    };
``` 

After a socket has been opened we will send a subscription to a resource:

```JavaScript
    socket.onopen = function(){
      console.log(sub);
      $scope.socket = socket;
      socket.send('sub ' + sub, socket);
      if (!quiet) {
        setInterval(function() { socket.send('ping'); }, INTERVAL);
      }
    };
```

Additionally some web servers silently time out if not periodically pinged so we send a ping message every 4 minutes.  If we get a message we check for the 'pub' command and if found we will fire a callback for further processing.

```JavaScript
    socket.onmessage = function(msg) {
      var a = msg.data.split(' ');
      if (a[0] !== 'pub') return;
      processSocket(a[1]);
    };
```

When we get a message the server will tell us which resource updated.  So we can now drop the cache, notify the user and fetch the resource again.

```JavaScript
    socket.onmessage = function(msg) {
      var a = msg.data.split(' ');
      if (a[0] !== 'pub') return;
      processSocket(a[1]);
    };
```


More Coming soon ...


## See Also

* [Source Code](https://github.com/melvincarvalho/chess)
* [Live Demo](http://melvincarvalho.github.io/chess/)
* [Websockets](https://en.wikipedia.org/wiki/WebSocket)
