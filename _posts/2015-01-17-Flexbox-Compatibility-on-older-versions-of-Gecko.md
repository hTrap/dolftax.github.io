---
layout: post
category : Applait
title : Flexbox Compatibility on older versions of Gecko
tagline: ""
tags : [Applait, Firefox OS]
---

Well, flexbox gives us a whole raft of new ways of controlling layout and flow. What we now achieve with floats we can do far more successfully and with more control with Flexbox.

We used Flexbox in [Finder](https://marketplace.firefox.com/app/finder). Because, [http://blog.applait.com/93](http://blog.applait.com/93).

Everything was fine on Firefox OS versions above 1.3, but on versions before that, the UI was scrambled. Eventually, it was evident that flexbox was fully supported only after versions 1.3 ( >= Gecko 28).

A complete CSS rewrite didn't make any sense. Customizing the rules based on the feature detection seemed to be a better option. We ended up with [Modernizr](http://modernizr.com/) - a javascript-driven feature detection library which adds classes to the HTML element based on the features it detected. Those classes could be used in css to define the alternative rules.

The flow would be like 1) Modernizr detects for features, 2) If flexbox is supported, usual CSS rules would be loaded 3) If flexbox is not supported, alternate rules under `no-flexbox` class, (added by modernizr), would be loaded.

{% highlight css %}

/** For instance, if modernizr detects, flexbox is not supported,
it adds classes like this. */

.no-flexbox #id {
    // Your alternate rule here
}

{% endhighlight %}

In latter case, to make the properties compatible, vendor prefixing (in our case, adding -moz to the properties) is the solution. In most cases, vendor prefixing would solve compatibility issues. But in our case, the UI was still scrambled. Because, the older flexbox implementation did not auto calculate element width. Defining the element width manually( example shown below), fixed it all.

{% highlight css %}

/** Example code - set width manually for elements*/
.no-flexbox #resetbtn {
width: 80%;
}

.no-flexbox #searchresults {
width: 100%;
}

{% endhighlight %}

Here is the CSS - [https://github.com/applait/finder/blob/v2.2.0/css/app.css](https://github.com/applait/finder/blob/v2.2.0/css/app.css) and the complete source code - [https://github.com/applait/finder](https://github.com/applait/finder)
