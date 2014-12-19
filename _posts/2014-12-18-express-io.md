---
layout: post
title: Express.io
---

##Introducing... [Express.io](http://express-io.org/)!

###The power of Express.js with WebSockets
I've recently started a new project that requires something a little different from the usual MEAN stack. I needed to route static resources (easy, with the power of Express.js) but I also needed to
manage WebSocket connections for a thick-client setup. I found that while Express.io essentially takes the same amount of time to setup, it has syntactical sugar benefits that were beneficial to the project in the long run.

###Examples
Let's look at examples of separate Express.js/Sockets.io, and then Express.io.

###Express.js + Sockets.io
```
var express = require('express');
var app = express.createServer();
var io = require('socket.io')(app);

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});

app.listen(80);
```

###Express.io
```
app = require('express.io')()
app.http().io()

// Setup the ready route, and emit talk event.
app.io.route('ready', function(req) {
    req.io.emit('talk', {
        message: 'io event from an io route on the server'
    })
})

app.listen(7076)
```

*I omitted the static file serving code from both because they were the exact same.*

###Thoughts
You will notice that combining Express.js and WebSockets.io uses essentially two different vocabularies - **app.get(dir, route)** for a Express route, and **io.on(socketEvent, callback)** for a WebSocket event. While not totally jarring, it did not hold a candle to the smoother Express.io **app.get()** and **app.io.route()**. I also liked that app.io.route callbacks mimicked the res.send() methods I had grown so accustomed to. 

Any cleaner routing is a win in my book!

###Bonus Round - "Realtime Routing"
Express.io features something it calls "Realtime Routing" - essentially the ability to route within a route!

**From the express.io GitHub page:**

```
app.io.route('customers', {
    create: function(req) {
        // create your customer
    },
    update: function(req) {
        // update your customer
    },
    remove: function(req) {
        // remove your customer
    },
});

And then on the client you would emit these events:
    customers:create
    customers:update
    customers:delete
```

Scaffolding for me has always been a subtle pain, and I expect to have to wire a lot of connection a lot in the coming weeks. I look forward to using Express.io to slide through with ease!
