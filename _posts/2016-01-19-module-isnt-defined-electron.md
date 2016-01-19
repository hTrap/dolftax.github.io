---
layout: post
category : General
title : "Resolving `module isn't defined` error in Electron"
tagline: ""
tags : [JavaScript, Electron]
---

Well, I got a chance lately to build a desktop app for [DoSelect](https://doselect.com) and we came across this weird issue

> moment not defined

We use moment.js for a couple of things. One of the answer from Stack Overflow suggested to turn `node-integration : false` but we needed node-integration for some other purposes. So, what/where is the problem?

`module` is defined, even in the browser-side scripts. This causes moment.js to ignore the window object and use module, so the other scripts won't find moment in global scope. When node-integration is true, moment.js sees that it is running in a CommonJS environment and expects to be used as such.

After looking into the following code ..

{% highlight javascript %}
//! moment.js
//! license : MIT
//! momentjs.com
.
.
.
function makeGlobal(shouldDeprecate) {
  /*global ender:false */
  if (typeof ender !== 'undefined') {
    return
  }
  oldGlobalMoment = globalScope.moment
  if (shouldDeprecate) {
    globalScope.moment = deprecate(
      'Accessing Moment through the global scope is ' +
      'deprecated, and will be removed in an upcoming ' +
      'release.',
      moment)
  } else {
    globalScope.moment = moment
  }
}
.
.
.
if (hasModule) {
  module.exports = moment
} else if (typeof define === 'function' && define.amd) {
  define('moment', function (require, exports, module) {
    if (module.config && module.config() && module.config().noGlobal === true) {
      // release the global variable
      globalScope.moment = oldGlobalMoment
    }
    return moment
  })
  makeGlobal(true)
} else {
  makeGlobal()
}
{% endhighlight %}

.. it is evident that, the issue is because `globalScope.moment = moment` is not being set because the conditons ended up true which resulted in `window.moment` returning `undefined`

Solution would be, loading moment.js via require instead of script tag. Like this,

{% highlight javascript %}
window.moment = require('/path/to/moment.js')
{% endhighlight %}

Cheers!
