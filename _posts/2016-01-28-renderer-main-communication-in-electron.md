---
layout: post
category : General
title : "Renderer - Main process communication in Electron"
tagline: ""
tags : [JavaScript, Electron]
---

[Electron (or) Atom Shell](http://electron.atom.io) is used to build cross platform desktop apps with web technologies. With electron, you can do a lot more than just wrapping your webpage into an app. In browsers, web pages usually run in a sandboxed environment and are not allowed access to native resources. Electron have the power to use Node.js APIs in web pages allowing lower level operating system interactions. Well, how does this work?

Electron exposes `ipc` module which allows you to communicate with the operating system. If you have worked with [socket.io](http://socket.io) , the pattern looks similar. `ipc` works based on [Event Emitter](https://nodejs.org/api/events.html) architecture.

Consider an example case where you got a webpage which when accessed from the app, should display the list of folders in a given directory, but from browser, should say "You gotta install our app for this feature".

First, let's detect whether the loaded environment is browser (or) app. In the webpage check this condition, `if(typeof process === 'object')`. When on app, this would return true. If in browser, false.

{% highlight javascript %}
if(typeof process === 'object') {
  var ipcRenderer = require('electron').ipcRenderer

  ipcRenderer.send('listDir', '/')

  ipcRenderer.on('listDirSuccess', function(event, arg) {
    // Log the list of files/directories to the console
    console.log(arg)
  })
} else {
  console.log('You gotta install our app for this feature')
}
{% endhighlight %}

In the above code, if the context is app, you emit `listDir` event to the main process and are listening for `listDirSuccess` event, which when occurs, you display whatever is being recieved. Simple! Now, let's listen for the `listDir` event in the Main process.

{% highlight javascript %}
var ipcMain = require('electron').ipcMain
var fs = require('fs') // To read the directory listing

ipcMain.on('listDir', function(event, arg) {
  fs.readdir(arg, function(err, files) {
    event.sender.send('listDirSuccess', files)
  })
})
{% endhighlight %}

In the application's index script, listen for `listDir` event, which when emitted, read the specific directory in the file system and emit `listDirSuccess` event with the array of files/directories.

With ipc module, you could do a lot more when the webpage is accessed from application(electron) context and make use of almost all the system level APIs which Node provides.

Go make the most out of electron. Cheers!
