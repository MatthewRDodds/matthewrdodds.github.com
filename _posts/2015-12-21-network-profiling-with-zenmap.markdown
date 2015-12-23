---
layout: post
title:  "Beginner Zenmap (Nmap)"
date:   2015-12-21 08:26:00 -0600
categories: react
desc: Using Zenmap to profile local wifi network
keywords: zenmap, nmap, web, internet, networking, security, network
---
Nmap is an incredibly useful tool for scanning networks and mapping out topologies. Nmap works by sending specifically crafted frames to all the target IPs in the specified range, the responses to these packets reveal information about the network. Nmap is able to map out the local network in this way.

Nmap has a GUI version available, called Zenmap, on Mac OSX. From my very limited experience I strongly prefer using the graphical version.

My need for using Nmap arose out of a realization that comcast (you suck, comcast) is now charging fees if you go over 300gb in a month, which I surpassed yesterday. So I want to ensure it is only I using the connection.

So what I wanted is a network view of all the connected nodes on my network. What tool can do this? Nmap!

After firing up Zenmap, I didn't read any tutorials, just adjusted settings until I got the result I wanted. What ended up working is finding my Router IP (`System Preferences > Network > Advanced > TCP/IP`) and plugging that into a range.

Zenmap shows you the nmap command that is run for the report, so for me the working command was `nmap -T4 -A -v 10.0.0.0/24` The `/24` turns this into a range of targets. It will scan all 256 possible values for the last (host) octet.

![Zenmap Results]({{ site.url }}/images/zenmap-results.png)

The end result was a brilliant report of all nodes on the network, OS profiling included. I was thoroughly impressed by how simple and easy it was to accomplish this. I was able to distinguish my router, my macbooks, my chromecast, and my xbox. In doing this I verified that no unauthorized devices were using my network.

So it is apparently entirely my fault for exceeding Comcast's stupid new data cap.
