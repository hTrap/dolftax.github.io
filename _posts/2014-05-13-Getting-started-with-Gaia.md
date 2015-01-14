---
layout: post
category : Mozilla
title : Getting Started with Gaia
tagline: ""
tags : [Mozilla, Firefox OS]
---

Let us dive deep into Gaia. But wait! Before getting started, let us look into the architecture.,

![](/images/firefox_os_architecture.png)

>Image Source: MDN, licensed under [CC-BY-SA 2.5](http://creativecommons.org/licenses/by-sa/2.5/).

Bewildered with the architecture?? If yes, then., Firefox OS is of three-layered architecture. The base being the low level linux kernel (i.e.,) Gonk and above that lies Gecko,a layout engine which reads HTML, CSS, JS, XUL, etc and render it. And at the top level, lies Gaia which is the User-Interface for Firefox OS. Now look at the above image.

Gaia is written with web technologies like HTML, CSS and Javascript. If you are pretty good with these, proceed further!

##Hacking with Gaia

You need 'git' now. Install git by running

    sudo pacman -S git

(or)

    sudo apt-get install git

(or)

    sudo yum install git

w.r.t your package manager.

Traverse to your development directory and clone the Gaia repo from git, but wait, we are planning to submit changes to gaia, right? Well, fork it then!
And clone the forked repo

    git clone https://github.com/your_username/gaia.git

<center><h2>Get some Caffine! A nap, might be!</h2></center>

This will take even an hour as the repo is pretty huge.

##Directory Structure

Start with your apps. The directory structure will be like

    manifest.webapp file: To store metadata about the app.
    style folder: To store CSS files.
    js folder: To store JavaScript files.
    locales folder:  To store translated strings for different languages.
    An HTML file: usually index.html.

Read the coding style which we follow, <a href="https://developer.mozilla.org/en-US/Firefox_OS/Platform/Gaia/Hacking#Coding_style_basics">here</a>.

If you got a Keon developer device, continue reading or drive [here](#emulator)

##Setting Up the Device

Download <a href="http://downloads.geeksphone.com/keon/master/nightly-images-keon-master-2014-05-12.Gecko-849b0f7.Gaia-014d16e.zip">b2g nightly build for Keon</a>. 

Oops! Let us set-up the system first. Download <a href="http://developer.android.com/sdk/index.html">adt bundle</a>. I would prefer to download SDK tools and then download platform-tools and build-tools, as the ADT bundle consists of too many extra packages as we don't need 'em in our case. Extract the bundle to /opt/android-sdk and change the directory rights

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

You've got the zip file of Keon nightly build of b2g. Unzip it, traverse into the folder and run 

    ./flash.sh

Wait until the device restarts. Alright, Into Gaia now!

##Make gaia

We've got the Gaia repo let us push it into the device. Traverse to Gaia repository and as of now, Keon uses the v1.0.1 branch of Gaia code, we will set the branch by,

    git checkout -b v1.0.1

Now,

    make install-gaia

Okay! Now, stop being lazy and get all [GOOD FIRST BUG]s <a href="http://www.joshmatthews.net/bugsahoy/?b2g=1">here</a>.

Choose a bug, think! Check with the code, make changes to the code, and again

    make install-gaia

Now, you can view the changes you made, live on your device!

If you're working on a specific app and made changes only on it, then to push the changes only for the app, run

    APP=calendar B2G_SYSTEM_APPS=1 make install-gaia

>Replace 'calendar' with the app_name you are working on.

More on make options <a href="https://developer.mozilla.org/en-US/Firefox_OS/Platform/Gaia/Hacking#Make_options">here</a>.

If you're interested to debug Gaia on Firefox Desktop, else -> [here](#end)

##Debugging Gaia with Firefox Desktop <a name="emulator"></a>

Download <a href="http://nightly.mozilla.org/">Nightly build of Firefox</a>. You've got Gaia already. No big deal! Traverse to Gaia repository and run

    /path/to/firefoxnightly -profile /path/to/B2G/gaia/profile-debug -no-remote

Done! This will open Firefox. You can see Gaia along with the<a href="https://developer.mozilla.org/en/docs/Tools"> devtools</a>. Make changes to the code, see it live on a "refresh".

Okay! Now, stop being lazy and get all [GOOD FIRST BUG]s <a href="http://www.joshmatthews.net/bugsahoy/?b2g=1">here</a>.

<a name="end"></a>

One last question! Have you got linux? The article is based on Linux. If no, <a href="http://jaipradeesh.github.io/arch/2014/05/06/Arch-Linux-Do-It-Yourself.html#sthash.KfcYbZUq.dpbs">here</a> then. You think Arch is complex??, get <a href="http://fedoraproject.org/en/get-fedora">Fedora</a>.

Stuck somewhere? Comment below with the issue. Before you are at beck and call, next blogpost on "Submitting Patches" will be up ;)

Cheers!
