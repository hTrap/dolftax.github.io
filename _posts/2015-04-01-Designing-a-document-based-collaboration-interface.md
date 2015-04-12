---
layout: post
category : General
title : "[Draft 1] Designing a document based collaboration interface"
tagline: ""
tags : [UI, Design]
---

This post is about my way of approach to develop User Interface for a document based collaboration platform. The Ideation is based on Martin's thoughts, which you can find it here - [http://societyserver.org/Topics/sTeam/Interface-elements-for-Document-Management](http://societyserver.org/Topics/sTeam/Interface-elements-for-Document-Management) . I would ask you to read the post and be back here.

> The structure lives and evolves. and so do the documents. - Martin

Alright, You're back! The primary goal was not to develop a separate admin panel. Rather the interface adds up extra admin options based on the permissions given to the logged-in user (Maybe, admin). 

> When I say `admin`, it means the authorized user who has Read/Write permissions and `guest` stands for non-authorized user who has only Read permissions.

As quoted, everything here would be documents, of any type (images, plain text, source code, ..) They should be structured into hierarchies. The admin/authorized user should be able to add new room, able to sort by Title/Author/Date, able to Re-arrange the documents, implemented as drag and drop.

![Home | Admin	 && User ](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/1.png)

Each room should have

- Topic
- Description
- Keywords 

and good to have various other attributes which might explain the room well. The admin has a sidebar which options to perform CRUD (Create/Read/Update/Delete) operations on a room. The sidebar is hidden for guest user. The wireframe below is detailed/zoomed view of a room in the above image.

![Room - Detailed View | Admin](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/2.png)

Creating a room asks for Room specific information. If you look at the wireframe below, they are self-explanatory. Permission would be set at this level whether it could be Shared/Private.

![Create room](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/11.png)

On click of a Room/Topic opens up the sub-topics under the room. The listing could be sorted and searched. Communication, being one of the major element for collaboration would be of comments. The admin gets to moderate (Approve/Delete) the comments. At this level, the comments are room-specific.

![onClick of Room | Admin](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/4.png)

You should have noted the `>>` on the right. It opens up a sidebar with Room/Topic listing which then nests into Sub-topic listing. These are the doors which helps the user for hassle-free navigation between rooms.

![Sidebar navigation - Right](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/6.png)

The sub-topic ( as same as Topic) has description, keywords and various other attributes. The sidebar of options and `Add Sub-topic` for admins to perform CRUD operations on them. The Sub-topic sidebar would be hidden for guest user.

![Sub-topic Detailed View](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/7.png)

Considering the hierarchy as a tree, the leaf node be the document. A document could be of any type,

- markup-text (markdown, html, others)
- xml, json, csv
- source-code
- image
- audio
- video
- binary
- object (instance of a script)

Displaying the content of a document in the browser would be based on the type of the document. Anything text based, images and videos are displayed. For other binary files or objects, only metadata is displayed (owner, date of creation etc). And binaries would have a download link. Comments at this level is document specific. 

> At any level, one should be able to navigate to any room/topic (or) sub-topic with the help of the right sidebar drawer.

The admin has the following options for each document,

- Link
- Copy
- Edit
- Curate (based on document type)

.. whereas guest would have everything else other than `Edit`.

Link icon pops up a list of Rooms (where the present logged in user has access to) which on click results in adding a link of the document to the respective room. Edit icon opens up the editor only if the document type is of something which could be edited in a browser. A complete document could also be deleted. The interesting part is to distinguish the documents based on the document-type, visually. The `Curate` icon pops up the list of documents in the specific room which are of the same document type as the currently viewed one.

![Document View - Admin](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/9.png)

A document would be displayed like the below wireframe for a guest user.

![Document View | User](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/10.png)

Creating a document asks for document specific information and feature for uploading the document. I assumed MIME-Type would be automatically detected. Else, an option could be added. Permission could also be set at document level.

![Create Document](https://raw.githubusercontent.com/dolftax/dolftax.github.io/master/sTeam/wireframes/12.png)

With that said, if you have any suggestions (or) if I'm missing something here, please start the discussion below. Note that these are bare minimum wireframes and therefore would be slightly modified during implementation. 

#### UPDATE: Uh oh! I missed containers. Expect a bit of restructure in my next draft.

Cheers!