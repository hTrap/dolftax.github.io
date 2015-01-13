---
layout: post
category : Mozilla
title : Servo, a brand new web browser engine
tagline: ""
tags : [servo,mobile,rust]
---

Servo is written using Rust, a new safe systems language developed by Mozilla. Rust has been development for several years now and is said to be rapidly approaching stability. Also, like C++, it is said to have efficient high-level, multi-paradigm abstractions, and offers precise control over hardware resources.

Now Mozilla, in collaboration with Samsung, is bringing Servo and Rust to Android and the ARM platform. Samsung has already contributed an ARM backend to Rust and the build infrastructure necessary to cross-compile to Android, along with many other improvements.

![Samsung_Mozilla_Rust.jpg](/images/samsung_mozilla_rust.jpg)

One may wonder what Samsung has to gain from this but the current browser in Samsung’s Android phones is made by Google, and is one of the few relatively stock apps on Samsung devices. With Google having directed its attention from developing the stock browser to Chrome, Samsung was faced with the choice of sticking with the old (and eventually to become outdated) stock browser, adopt Chrome (which is still floundering; not to mention having to rely on Google again) or make something of their own. As such, it’s easy to see why they went with the last option.

It does make one wonder about the future of web development, though. With most companies using WebKit, a sense of uniformity had emerged but now it seems things could get difficult for web developers again, if at all Samsung chooses to adopt Servo on a wide scale.