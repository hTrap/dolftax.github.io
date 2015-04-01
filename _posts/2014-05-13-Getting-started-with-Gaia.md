---
layout: post
category : Mozilla
title : Getting Started with Gaia
tagline: ""
tags : [Mozilla, Firefox OS]
---

Let us dive deep into Gaia. But wait! Before getting started, let us look into the architecture.

![](/images/firefox_os_architecture.png)

>Image Source: MDN, licensed under [CC-BY-SA 2.5](http://creativecommons.org/licenses/by-sa/2.5/).

Bewildered? Firefox OS is of three-layered architecture. The base being the low level linux kernel (i.e.,) Gonk and above that lies Gecko, a layout engine which reads HTML, CSS, JS, XUL, etc and render it. And at the top level, lies Gaia which is the User-Interface for Firefox OS.

Gaia is written with web technologies like HTML, CSS and Javascript. If you are pretty good with these, you could proceed further, else I would recommend you to get the basics strong before you hack on Gaia.

##Hacking with Gaia

Gaia repository is mainained with 'git' as VCS. Install git by running

    sudo pacman -S git

(or)

    sudo apt-get install git

(or)

    sudo yum install git

w.r.t your package manager.

Traverse to your development directory and clone the Gaia repo from git, but wait, we are planning to submit changes to gaia, right? Well, fork it then!
And clone the forked repo

    git clone https://github.com/your_username/gaia.git

Get some Caffine! Maybe a nap! This would take even an hour as the repo is pretty huge.

##Directory Structure

Start with your apps. The directory structure will be like

    manifest.webapp file: To store metadata about the app.
    style folder: To store CSS files.
    js folder: To store JavaScript files.
    locales folder:  To store translated strings for different languages.
    An HTML file: usually index.html.

Do read the coding style and conventions <a href="https://developer.mozilla.org/en-US/Firefox_OS/Platform/Gaia/Hacking#Coding_style_basics">here</a>.

##Setting Up the Device

Let us set-up the system first. Download <a href="http://developer.android.com/sdk/index.html">adt bundle</a>. I would prefer to download SDK tools and then download platform-tools and build-tools, as the ADT bundle consists of too many extra packages as we don't need 'em in our case. Extract the bundle to /opt/android-sdk and change the directory rights

    chmod -R 755 /opt/android-sdk

Now configure udev rules. Copy the below rule to /etc/udev/rules.d/51-android.rules file

    SUBSYSTEM==”usb”, ATTR{idVendor}==”05c6”, MODE=”0666”, GROUP=”plugdev”

>You might need to restart your system to refresh the new rules

Get it going! Plug-in your device, turn ON 'remote debugging' and 'screen timeout' to NEVER. 

>Don't forget to set PATH variables to /opt/android-sdk/platform-tools. Need help? Find it <a href="http://bit.ly/1jbjMEl">here</a>

Test it out.

    adb start-server
    adb devices

This should show you full_keon (or) keon_device or whatever under "List of Devices attached"

Download <a href="http://downloads.geeksphone.com/keon/master/nightly-images-keon-master-2014-05-12.Gecko-849b0f7.Gaia-014d16e.zip">b2g nightly build for Keon</a>.

You've got the zip file of Keon nightly build of b2g. Unzip it, traverse into the folder and run 

    ./flash.sh

Wait until the device restarts. Alright, Into Gaia now!

##Make gaia

We've got the Gaia repo let us push it into the device. Traverse to Gaia repository and read `README.md` and `CONTRIBUTING.md` files thoroughly. You could also read through https://developer.mozilla.org/fr/Firefox_OS/Platform/Gaia/Hacking

To get started, those relatively easy and mentored bugs are tagged with [GOOD FIRST BUG] Find such bugs <a href="http://www.joshmatthews.net/bugsahoy/?b2g=1">here</a>.

If you are comfortable with the bug, please assign it to yourself. Create a local branch

    git checkout -b "bugNumber-bugStatement"

As explained in the bug, tweak the code, add a feature (or) fix a bug. To test it out in a device, run

    make install-gaia

Check with the code, make changes to the code, and again run

    make install-gaia

Now, you can view the changes you made, live on your device!

If you're working on a specific app and made changes only on it, then to push the changes only for the app, run

    APP=calendar B2G_SYSTEM_APPS=1 make install-gaia

>Replace 'calendar' with the app_name you are working on.

Find more about make options <a href="https://developer.mozilla.org/en-US/Firefox_OS/Platform/Gaia/Hacking#Make_options">here</a>.

##Debugging Gaia with Firefox Desktop

Download <a href="http://nightly.mozilla.org/">Nightly build of Firefox</a>. You've got Gaia already. No big deal! Traverse to Gaia repository and run

    /path/to/firefoxnightly -profile /path/to/B2G/gaia/profile-debug -no-remote

Done! This will open Firefox. You can see Gaia along with the<a href="https://developer.mozilla.org/en/docs/Tools"> devtools</a>. Make changes to the code, see it live on a refresh.

##Initiating a Pull Request(PR)

When changes are made to the code as per the bug, open your fork on github.com. You would get a button `Send Pull Request`. Click on it and fill up the necessary fields. And Create a Pull Request. Initiate r? to your mentor (In Bugzilla) with the Pull request link. Now, the module peer (or) mentor would make necessary comments on the bug.

When everything goes well, your pull request would be merged to the codebase. Weeh!

The article was drafted assuming you got Linux. If no, you could try installing it with the help of the setps mentioned <a href="http://jaipradeesh.github.io/arch/2014/05/06/Arch-Linux-Do-It-Yourself.html#sthash.KfcYbZUq.dpbs">here</a>.

Stuck somewhere? Please be specific and comment below!

Cheers!
