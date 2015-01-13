---
layout: post
category : Mozilla
title : Get the GPS more accurate on tarako devices
tagline: ""
tags : [FirefoxOs,b2g,tarako]
---

Tarako devices has got A-GPS (Assisted GPS) and it has to lock the position with the help of the pre-configured SUPL server. In tarako, it takes too much of time to lock the position. The reason behind this delay is because of the bad SUPL server which is configured in these devices. So, changing the SUPL server configuration locally is the thing we need to do here.

Connect your device, enable USB debugging and do the following.

    adb pull /system/b2g/defaults/pref/user.js

then edit user.js, replacing:

    pref("geo.gps.supl_server", "supl.izatcloud.net");
    pref("geo.gps.supl_port", 22024);

with:

    pref("geo.gps.supl_server", "test.supl.svc.ovi.com");
    pref("geo.gps.supl_port", 7276);

and, finally:

    adb remount
    adb push user.js /system/b2g/defaults/pref/user.js
    adb reboot

This will reduce the time taken to lock the position.

PS: This applies for Geeksphone Keon and Peak too.
