---
layout: post
category : General
title : Insights on app for an event/conference
tagline: ""
tags : [Webapp]
---

An app for event play well because it makes things easy for the end user by pushing features to notify, update and engage himself to the event.

I figured out the following list would the vital ones for event app.

- Session/Agenda listing
- Floor plan / Map
- iCal generation
- Survey form
- Comments on each session listing
- Speaker info
- Forum on generic topics related to the event
- Hashtag grep | Facebook && Twitter
- Push notifications for announcement

Considering the major features needed for the application, almost none of them depend much on the system. If you check Cordova Platform Support page -  [http://cordova.apache.org/docs/en/4.0.0/guide_support_index.md.html#Platform%20Support](http://cordova.apache.org/docs/en/4.0.0/guide_support_index.md.html#Platform%20Support) [1] , even the push notification is supported and are supplied as plugins.

It would be very much better and intuitive way to go with web application (Responsive) and wrapping it up with Cordova (Any good alternative? Comment below!) and thus making it platform independent.

The whole point of the application is that it should not be so much of system/platform dependent and should run everywhere as expected. Interesting part is Cordova support is increasing rapidly in recent days. If you check the above link [1], the API (as Plugins) support list goes all green with Amazon Fire OS, Android, Blackberry, Firefox OS, iOS, Ubuntu, Windows OS and some goes green with Tizen as well.

Native apps works well if we are using system resources heavily for rendering objects. With that said, it is good to learn from others.Check out Google I/O application ( [https://play.google.com/store/apps/details?id=com.google.samples.apps.iosched&hl=en](https://play.google.com/store/apps/details?id=com.google.samples.apps.iosched&hl=en) ) to get overview and clear idea of the important aspects to be considered when designing && developing an event application.
