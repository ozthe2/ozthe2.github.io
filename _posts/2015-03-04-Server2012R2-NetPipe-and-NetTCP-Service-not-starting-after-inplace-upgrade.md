---
layout: post
title:  "Server2012R2: Net.Pipe and Net.Tcp Service Not Starting After In-Place Upgrade to Server 2012R2"
date:   2015-03-04 22:00:00 +0000
categories: Server2012R2
tags: [server2012, Server2012r2, server2008, server2008r2, upgrade]
---
Having just performed an in-place upgrade from Server 2008R2 to 2012R2 on two of our DHCP servers, I noticed the following two errors in Server Manager once the upgrade was complete:

![1-5](/assets/images/1-5.PNG)

When Clicking on the Services link I was presented with the information that Net.Tcp Listener Adapter and the Net.Pipe Listener Adapter services could not be started.

When I checked the services it could clearly be seen that they were set to automatic but had not started.  Manually trying to start the services would not work either.

![2-4](/assets/images/2-4.PNG)

The solution was in two parts.  The first was to fully patch the server – on checking I found the server had 41 updates required.

Once I had patched and restarted the server, I only had one error in Server Manager:

![a](/assets/images/a.PNG)

The only error now was showing that the Net.Tcp Listener Adapter service was in a stopped status:

![b](/assets/images/b.PNG)

When I tried to start it manually I received the following error:

![3-4](/assets/images/3-4.PNG)

I checked the Event log and found the following information:

![4-4](/assets/images/4-4.PNG)

Cool – now we’re getting somewhere.. I needed to start the Net.Tcp Port Sharing Service.  When I checked, it was indeed disabled.
I set it to automatic:

![5-4](/assets/images/5-4.PNG)

Once that was done, I attempted to start the Net.Tcp Listener Adapter service again:

![6-3](/assets/images/6-3.PNG)

Success!

![7-3](/assets/images/7-3.PNG)