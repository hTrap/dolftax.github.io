---
layout: post
category : General
title : "Node.js clustering maintaining sticky session"
tagline: ""
tags : [JavaScript, Scaling]
---

NodeJS is single threaded. It is event-driven and single-threaded with background workers. Scaling up a node application is possible by splitting a single process into multiple processes or workers by using [cluster](https://nodejs.org/api/cluster.html) module. The cluster module allows you to create child processes (workers), which share all the server ports with the main Node process (master).

A simple example

{% highlight javascript %}
var cluster = require('cluster')
var http = require('http')
var numCPUs = require('os').cpus().length // Number of cores in your machine

// Initiate master process
if (cluster.isMaster) {

  // .. which in turn initialize the workers
  for (var i = 0; i < numCPUs; i++) {
    cluster.fork()
  }
} else {
  // Application code
  http.createServer(function(req, res) {
    res.writeHead(200)
    res.end(process.pid + ' says hello!')
  }).listen(8000)
}
{% endhighlight %}

.. the above would run per process per core and works well for all applications except the ones using WebSockets.

A WebSocket connection would do multiple requests to perform handshake and establish connection with a client. With a cluster those requests may arrive to different workers, which will break handshake protocol. Sticky-sessions module is balancing requests using their IP address. Thus client will always connect to same worker server, and socket.io will work as expected, but on multiple processes.

{% highlight javascript %}
var sticky = require('socketio-sticky-session')

var options = {
  proxy: true, // Activate layer 4 patching
  num: require('os').cpus().length
}

var server = sticky(options, function() {
  // This code will be executed only in slave workers

  var http = require('http')
  var io = require('socket.io')

  var server = http.createServer(function(req, res) {
    // ....
  })

  io.listen(server)

  return server
}).listen(3000, function() {
  console.log((cluster.worker ? 'WORKER ' + cluster.worker.id : 'MASTER') + ' | HOST ' + os.hostname() + ' | PORT ' + 3000)
})
{% endhighlight %}

If anything above doesn't seem to work, do comment. Will answer 'em o/
