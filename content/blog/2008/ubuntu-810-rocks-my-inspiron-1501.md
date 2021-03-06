---
title: Ubuntu 8.10 rocks my Inspiron 1501
date: "2008-11-01"
url: /blog/2008/11/01/ubuntu-810-rocks-my-inspiron-1501/
categories:
  - Desktop
  - Open Source
---
I'm really really happy about [Ubuntu 8.10](http://www.ubuntu.com/) because it lets me stop kicking myself so much for buying a Dell Inspiron 1501. This little laptop was the el-cheapo option for me, found via [dealnews.com](http://www.dealnews.com/). I was going to buy the virtually identical one that came with Ubuntu installed, but then Dell offered a deal on the 1501, which had Windows Vista, and I caved in to the allure of saving about $200.

Of course I promptly discovered that the two most important differences between the models involved hardware for which no good Free Software drivers existed: the video card and the wireless card. The Inspiron 1501 has a "ATI Technologies Inc RS482 [Radeon Xpress 200M]" and a "Broadcom Corporation BCM4311 802.11b/g WLAN (rev 01)".

<!--more-->

I use dual monitors; it's pretty much a necessity for me. And I just couldn't get the radeon driver to work right with them. I spent a lot of time trying. I ended up going to the ATI driver, which is proprietary; it had its own issues with mouse pointer corruption and the lot, which eventually were fixed, but it still disabled suspend/resume, and plus it's non-Free. My colleagues know this irked me---they just heard me griping about it a few days ago.

But now, praise be, the radeon driver works with my dual monitors! And the drag-and-drop point-and-click configuration interface works, too! I've got a 1680x1024 external monitor, positioned above my 1024x800 laptop display, and I have never so much as peeked at /etc/X11/xorg.conf. Thanks to all the people who worked so hard on this! (It didn't work flawlessly until I rebooted, but who's complaining.) Suspend/resume now work great!

I haven't gotten the wireless card working yet; the bw43-cutter package seems to have disappeared. But I'm actually hoping that I won't need proprietary drivers for this, too.


