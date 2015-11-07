---
layout: post
title:  "Mac Address Spoofing"
date:   2015-11-06 23:17:33 -0600
categories: security
---
The first thing I wanted to figure out that how to spoof my mac address. While this was easy to do on OS X with the default adapter, it was actually a difficult ordeal with [no resolution](http://apple.stackexchange.com/questions/157204/how-to-spoof-a-usb-ethernet-adaptor-mac-address-in-os-x) for my Alfa 802.11 USB adapter.

I was however finally able to configure virtual box properly in order to be able to do this from my Kali linux VM:

{% highlight bash %}
root@kali:~-# ifconfig | grep HWaddr
eth0       Link uncap:Ethernet  HWaddre 08:00:27:95:4c:25
root@kali:~-# ifconfig eth0 down
root@kali:~-# ifconfig eth0 hw 08:00:27:95:4c:26
root@kali:~-# ifconfig eth0 up
root@kali:~-# ifconfig | grep HWaddr
eth0       Link uncap:Ethernet  HWaddre 08:00:27:95:4c:26
{% endhighlight %}

So progress and accomplishment and profit! 


## Lessons learned along the way:

While troubleshooting the wireless adapter and trying to be able to use it in Kali linux I was unable to enable it in the VM, and would get a “resource already in use” confirmation notice when I tried. I learned that the adapter’s driver that I had installed on OSX was causing the issue. Apparently there are .kext files down in `/System/Library/Extensions` and those essentially are kernel extensions / drivers for various hardware devices, so to disable the wireless adapter driver I just moved its associated `kext` to Desktop, and this worked. However Kali still wasn’t cooperating. I ended up disabling the default adapter for sharing with the VM and bridging my Alfa adapter instead, which is what actually ended up being the final solution.
