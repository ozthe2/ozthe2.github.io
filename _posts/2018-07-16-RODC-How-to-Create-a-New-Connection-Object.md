---
layout: post
title:  "RODC: How to Create a New Connection Object"
date:   2018-07-16 22:00:00 +0000
categories: RODC
tags: [rodc,connection]
---
There may come a time whereby you will need to create a new connection object for your RODC's due to someone inadvertently deleting the existing one by mistake, or having to deliberately delete and recreate the connection object as in [my case]({{ site.baseurl }}{% link _posts/2018-07-12-RepAdmin-Warning-KCC-could-not-add-this-replica-link-due-to-error.md %}).

Connection objects for RODC's require a quick 'tweak' in order to get them to function correctly.  If you don't, then they won't work.

Basically, you create your connection object as per normal, giving it the name *RODC Connection (SYSVOL)* if you are doing this for server 2012 or higher, or name it *RODC Connection (FRS)* for server 2008r2.

Then right-click the connection object you just created -> properties and select the *Attribute Editor* tab and in the *Options* attribute, enter *0x40* for the value:
![1RODC](/assets/images/1RODC.JPG)

That's it.

You *know* I'm not clever enough to just know all this right?  Right?  

Yeah... I got this information from here: [Clever people](https://support.microsoft.com/en-gb/help/3212965/events-6804-and-2843-are-logged-and-rodcs-do-not-replicate-sysvol)