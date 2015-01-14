---
layout: post
category : Mozilla
title : Uninstall Webapps from Desktop
tagline: ""
tags : [Mozilla, Firefox OS, Webapp]
---

>Steps to remove a webapp from Desktop [Linux only]

1) Traverse to your home directory

    cd ~
    ls -la

2) You will find folder like this application_namexxx

3) Remove the folder

    rm -rf application_namexxx

4) To remvove the app from 'Applications Menu' listing

    cd .cache
    ls -la
    rm -rf application_name
    cd ..
    cd .local/share/applications/
    rm -rf application_namexxx.desktop

You're done!


