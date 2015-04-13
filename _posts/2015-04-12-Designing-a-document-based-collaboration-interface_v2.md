---
layout: post
category : General
title : "[Second Draft] Designing a document based collaboration interface"
tagline: ""
tags : [UI, Design]
---

.. this post is the continuation of my first draft which you could find it here - [http://dolftax.com/2015/04/Designing-a-document-based-collaboration-interface/](http://dolftax.com/2015/04/Designing-a-document-based-collaboration-interface/) .  I would ask you to go through the first draft before proceeding here, because here I've explained only the wireframes which are modified/tweaked, based on the comments on the first draft. This post is structured as /me resolving the comments on my first draft, with the new wireframes and explaining the reasons for modification.

### Rooms could be nested

 #1 : We could not enforce a topic/subtopic structure because rooms can be deeply nested. Topics and subtopics are all rooms. The users are free to organize the rooms as they wish. They could be topics, they could be something else. At every level, there may be documents and more rooms.

=> Removed topic/subtopic structure. As the rooms are completely nested, a room could contain any number of sub-rooms. Rooms and documents are analogous to folders and files. But wait, there are containers which are multi-part documents. To get the clear idea of what we mean by containers- refer to the discussion we had | IRC log - [https://tr.im/UOZpT](https://tr.im/UOZpT)

### Shared and Private workarea

  #2: The basic elements in sTeam are users, groups, rooms and documents. Each group has a workarea connected to it, and each user has a private workroom. Each user is a member of at least one group. So when a user enters the server, there are at least two rooms: the users private workarea, and the workarea of the group, that the user is a member of.

=> Workarea implemented. Under shared workarea, the user will get list of all rooms and documents which he got access to. Under private workarea he would get list of his private documents and rooms, which when shared will move to the shared workarea.

#### Shared Workarea

![Shared Workarea - admin](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/home_admin_shared.png)

#### Private Workarea

![Private Workarea -admin](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/home_user_private_l1.png)

If you notice, you could create a room or document only in your private workarea. When you change permissions for a room/document in your private workarea, it would be pushed to shared workarea automatically.

> ##### Permissions are inherited
If a room has `rw` permissions, then everything inside the room also has rw permissions.

#### Room view - Level two

![Room View - Level two](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/home_user_private_l2.png)

Notice the `settings` icon? Except for the first level, (levels are tracked by the level/stage bar) a user could change room/document attributes with the help of `settings` icon which pops up a window with following options.

![Settings pop](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/settings_admin_popup.png)

>  The `settings` option appears only in the levels inner to level 1, because obviously, if the user is in the first level, he is not into any room.

### Navigation between rooms

 #3: The user can move from room to room. The server keeps track of where the user is, and actions taken (such as creating a document) are relative to the users location. Users can pick up documents (the document is moved from the room, to the user itself), move to another room and drop the documents there.

=> When a document is selected, the `copy` and `paste` buttons (look at the above wireframe. buttons next to sort options) are activated. Clicking copy would copy the selected document, and allows you to paste it in any room (where you got access to) until the end of the session. Navigation between rooms could be done by clicking `<<` button. It would popup the navigation sidebar on the right.

![Sidebar Right](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/sidebar_right-navigation.png)

Also, if you wish to join any room, use the search bar. It would fetch you the list of rooms. Some rooms will not allow you to access the documents. Click on the `user request` icon next to room name, which would notify the room admin. When he gives you access, the room/document would be displayed in your shared workarea. 

#### Search Results view

![Search Results](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/search_results.png)

### Permission table

 #4: A user should be able to insert objects without read and write permissions. 
One example where this is needed is to send your homework to your teacher.
You get permission to insert into the teachers room, but once it's in there,
you can't read it or write it anymore. It allows far more fine grained permissions than a unix system.

=> A permission button has been added to the 'onClick of a Room' view which will be available for the room admin and you.

![In room view - Admin](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/onclick_room-admin.png)

For an admin, the permission table pop-up would look like the below wireframe (which is self-explanatory)

![Permission table popup](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/permission-table.png)

### Minor tweaks

#### Room sidebar removed

The [room attached sidebar](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/2.png) options has been moved to the settings popup. A detailed view of a room in any level would look like,

![Room Detailed](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/room_detailed.png)

#### Document View

In document level view, the following options are added,

- Workarea bar
- Delete document option (If access permits)
- Permissions button

![Document View](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/document-admin.png)

#### Guest view

A guest (who is not logged in) could view the rooms/documents. The view for a guest would look like,

![Guest room view](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/onclick_room_guest.png)


PS: No changes have been made to [Create room](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/create_document.png) and [Create document](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/web_interface_v2_wireframes/create_room.png) pop-ups.

Let me know what you think!
