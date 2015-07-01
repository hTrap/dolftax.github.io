---
layout: post
category : General
title : "GSoC 2015 with FOSSASIA - Mid-term report"
tagline: ""
tags : [GSoC]
---

TL;DR No Chicken Little, the sky is not falling.

   Well. I've been selected for GSoC under organization FOSSASIA and I am working on the project sTeam Collaboration platform, mentored by awesome guys Martin and Aruna.

It is mid term already and as planned I am half way through the project. If you haven't seen my past blogposts, go check them out to get clear idea of the project. [sTeam](http://societyserver.org/Topics/sTeam/Interface-elements-for-Document-Management) is a document based collaboration platform. There is already an existing web interface for the platform. Interestingly REST APIs are being developed for the same and we planned to rewrite the web interface with AngularJS and make calls to the REST APIs.

### Technology stack

- `bower` for easy management of external modules. There are a lot of sub modules which are to be loaded and are not part of the angular itself. Though, some of the modules are bloated. The unnecessary files will be removed by using bower prune task with gulp.

- `angular-ui-router` for handling deep nested routes. Interesting thing is, angular-ui-router works on state based concept and is very handy to maintain and route to certain state.

- `angular-ui-bootstrap` gives us easy to use, clean and responsive UI blocks.

- `angular-local-storage` We use it for saving the user's login credentials and are sent to the API with every REST based call. This would be changed in future and session maintenace should be developed.

- `textAngular` is lightweight and two way bound WYSIWYG Text Editor for handling plain text files. It can also handle source code, markdown, etc ..

- `ng-audio` and `ng-video` for viewing audio and video files respectively.

### Views

- `login` and `workarea` are two base templates. And the router loads one of these based on the login credential value stored in local storage.

- With `workarea` as base template, at this level, two nested views. Groups, which displays the groups which the user is part of and Private, where the user's private documents are displayed.

- The `options` view has various options like, permission management for the current level, copy, link, etc.. and also create room and document modals.

- `comments` view fetches the comments for the current path. It is hidden if no permission to comment.

### Controllers

- `loginCtrl` for passing the credentials to the API, authenticate and parellely store them in localStorage. And all the other calls will use the stored value along with its payload. You know, REST is stateless! Session management is scoped to the API and is planned for future.

- `handler` has functions for CRUD operations on the API. The functions do GET, PUT, POST, DELETE, .. on the passed paramater (which is the path to the room/document) and will return the value.

- `router` handles the routes. It has base states with views loaded into each states with its own templates and controllers.

- The `run` methods load are used for state change control.

- `workareaCtrl` handles the scope for options loading and current level display in breadcrumb.

- `workspaceCtrl` fetches and controls the main workspace which has the rooms, documents and containers displayed.

- `config` has the hostname where the sTeam is deployed and change here is reflected systemwide for easy deployment. 

### Road ahead

- Depending on the type (room/document), the appropriate view should be loaded and when document, the viewer/editor wrt to the mime type should be loaded. Follow the issue here - [ https://github.com/dolftax/sTeam-web-interface/issues/10](https://github.com/dolftax/sTeam-web-interface/issues/10)

- Implement search, document/room sorting based on Author, Title, document type and date.

- Setup right sidebar which lists all the rooms (for easy navigation).

- Settings popup for changes to attributes of the objects.

- Automate tasks with certain gulp modules - gulp-angular-templatecache, gult-concat, gult-lint, gulp-uglify, ..

- Write unit tests with mocha and chai.

- Tidy up and add more documentation, which is already being done here - [https://github.com/eMBee/sTeam/wiki/Installation-steps](https://github.com/eMBee/sTeam/wiki/Installation-steps)

Apart, we do scrum meet everyday. Check out the logs - [http://dpaste.com/2A3J121](http://dpaste.com/2A3J121)

Currently, `node-static` module is used to serve the app and our development server is hosted in azure - [http://steam-web.azurewebsites.net/](http://steam-web.azurewebsites.net/)

>Note: The project is heavily under development and things might break.

Sign-up API is not implemented yet. Find some of the working screenshots below

![Login](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/screenshots/login.png)

![Private workarea](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/screenshots/private_workarea.png)

![Groups](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/screenshots/groups.png)

![Create room](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/screenshots/createroom.png)

![Create document](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/screenshots/createdoc.png)

### Future plans

The REST APIs are under development and a lot of features are yet to be developed. I have a brief listing of the yet to be developed APIs and the list grows eventually as we figure out something is missing.

Thats all for now. Will get back soon!
