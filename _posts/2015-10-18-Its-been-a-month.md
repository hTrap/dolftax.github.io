---
layout: post
category : General
title : "It's been a month .."
tagline: ""
tags : [DoSelect]
---

.. since I joined DoSelect. At DoSelect, I work on the JavaScript parts of the codebase. Prior, as Google Summer of Code dev, I revamped 
the API and web interface of Steam Collaboration Platform. I’ve helped build couple of small components at [Applait](http://applait.com). Also have been reviewing applications for Firefox Marketplace for almost 2 and a half years now. If you are aching to read more about me, here you go - [http://dolftax.com/about](http://dolftax.com/about)

I always wanted to work on somewhere/something where my work directly impact the product. If you take tech hiring, something is very wrong in the current flow. I completely agree with the statement “Don’t disqualify candidates based on stuffs like classic CS-101 algorithms, or any type of puzzle problem. What you really need to know is, “does this candidate understand how to put an application together?” which is 
exactly what DoSelect is trying to solve.

In the first week, I wanted to ship something, be it 0.1.0 Started off with wrapping up doselect.com into a web app. Electron was an 
obvious choice. But as we built the app, a couple of things was against the trivial rules of UX. For instance, the IDE was opening in a new 
window which ended up in establishing a poor relation between the dashboard and IDE. We looked at Slack and it handles the same scenario 
pretty well. Hold your horses until we hit 1.0.0

Currently, we are using Codebox as our IDE. We noticed, it was pretty heavy and an overkill for our use case. We didn’t want to reinvent the wheel, either. Figured out, we don’t need a lot of features which codebox has. Tried to scrape them from the code, but ended up in vain as their front-end and back-end were tightly coupled. Writing an IDE from scratch with front-end and back-end completely decoupled and make them talk through a REST interface seemed to be a better option. Altair and Desmond were born. We came a across a lot of interesting hindrances as we build this. Will write more about it later. Moving on, code (and git) conventions of course matters. Bender was born.

For us, every pixel matters! As we added more features, the main nav was pretty over populated. We didn’t want the ugly, big native scrollbars. Angular-perfect-scrollbar was a good choice. There was an Angular implementation but wait we saw this.

`<script src="../bower_components/jquery/dist/jquery.min.js">`

After examining why they committed this sin, [http://vanilla-js.com/](http://vanilla-js.com/) seemed to be a better option. We rolled out our first open source component [ng-perfect-scrollbar](https://github.com/doselect/ng-perfect-scrollbar).

How does a usual day look at DoSelect? Well, coffee, big screens, vim, tmux, git, food, Foosball, bad puns, JIRA, HN discussions, Slack, Cricket and food. Other usual things include, /me typing `git status` in Firefox window, Sanket doing `console.log` in app.py .. and I got along.

<iframe src="https://vine.co/v/eFwweQWYxDY/embed/simple" width="600" height="600" frameborder="0"></iframe><script src="https://platform.vine.co/static/scripts/embed.js"></script>

BTW, What on earth are Altair, Bender, .. ? Repository names.

> This was originally posted at [DoSelect Blog](http://blog.doselect.com)
