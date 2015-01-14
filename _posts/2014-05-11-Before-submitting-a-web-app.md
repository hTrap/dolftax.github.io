---
layout: post
category : Mozilla
title : Before Submitting a web-app
tagline: ""
tags : [Mozilla, Webapp]
---

Open web applications are likely to continue to gain acceptance by end users, and for developers, they are a way to monetize the skills that they already have. But actually, *3 out of 10 submissions* seems to lag in quality. Personally, while we review apps, we first look at the functionality of the app and then the code. I've gathered some points for developers for carving an awe-inspiring web-app.

##1.App Name, Description and Screenshot

Yes! It matters. Make the app name sensible, not too long (App name more than 20 characters will be truncated in mobile screens). When someone visits marketplace to download your app, the first thing he/she looks at will be the UI of the app which will be shown as screenshots in the download page. Check with the screenshot criteria [here](https://developer.mozilla.org/en-US/Marketplace/Publishing/Marketplace_screenshot_criteria). Let the description part be clear and likeable to your target audience. Make sure you mention about 1)Purpose of the app & 2)How it works (i.e., the functionaliy)
Take full advantage of the first few lines and gradually use the introductory words to succinctly tell your users what your app does and how will it benefit them and what makes them get excited about it. 

##2.Framing the mainfest

Apart from the proper syntax (because you cannot escape from the validator),do respect the description element of permissions. Use plain language to clearly describe the app's use of that permission. Never write words which are no-way related with the app's designated purpose. And also, including [appcache](https://developer.mozilla.org/en-US/docs/HTML/Using_the_application_cache) will fetch and parse the contect in local cache folder and will improve the swiftness of the app.

##3.App Icon

It's no coincidence that the best and most popular apps frequently have memorable icons.A good icon is critical piece of an app's design and has a huge effect on how people think about the app.In our case, the default rocketship icon is not allowed anymore. [Mozilla style guide](http://www.mozilla.org/en-US/styleguide/products/firefox-os/icons/) gets you icon design steps and icon underlays. Generally, 128x128px icon is for marketplace and 60 x 60px icon for display on the device.

##4.Responsive Design

>“If you're already a front-end developer, well, pretend you're also wearing a pirate hat.”
― Ethan Marcotte

Your app should extend all of its functionalities in large, medium and small screens. Most common suggestions for making your app responsive are 1) Precise UA sniffing: [https://developer.mozilla.org/en-US/docs/Gecko_user_agent_string_reference](https://developer.mozilla.org/en-US/docs/Gecko_user_agent_string_reference) 2)Similar client-side screen size detection methods: https://developer.mozilla.org/en-US/docs/CSS/Media_queries

I found this article to be interesting - [http://www.webdesignerwall.com/tutorials/5-useful-css-tricks-for-responsive-design](http://www.webdesignerwall.com/tutorials/5-useful-css-tricks-for-responsive-design)

Do think from user's point of view as the first 10 seconds of your app will decide the durability of your app. Let the button sizes be designed properly and  number of touchable UI elements be less than 10 per view.

##Essential Resources

[1] Manifest Reference- [https://developer.mozilla.org/en-US/Apps/Build/Manifest](https://developer.mozilla.org/en-US/Apps/Build/Manifest)

[2] Toolkits- [http://buildingfirefoxos.com](http://buildingfirefoxos.com/)

[3] Font Set- [https://github.com/mozilla-b2g/moztt/tree/master/FiraSans-2.001](https://github.com/mozilla-b2g/moztt/tree/master/FiraSans-2.001)

[4] Icon Set- [https://mozilla.box.com/s/jp5lrplbuont96ypm27q](https://mozilla.box.com/s/jp5lrplbuont96ypm27q)

Wait! These are the web-apps which can be put under "must download" category!

###[Loqui](https://marketplace.firefox.com/app/loqui) | [Twitter](https://marketplace.firefox.com/app/twitter) | [Vertigo](https://marketplace.firefox.com/app/vertigo) | [Washington Post](https://marketplace.firefox.com/app/the-washington-post) | [File Manager](https://marketplace.firefox.com/app/file-manager) | [Youtube](https://marketplace.firefox.com/app/youtube-1) | [Asteroid Blaster](https://marketplace.firefox.com/app/asteroid-blaster) | [Fishing Cat](https://marketplace.firefox.com/app/fishing-cat)###

