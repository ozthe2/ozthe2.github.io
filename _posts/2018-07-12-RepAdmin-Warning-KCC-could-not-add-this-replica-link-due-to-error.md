---
layout: post
title:  "REPADMIN - Warning: KCC could not add this REPLICA LINK due to error"
date:   2018-07-12 22:00:00 +0000
categories: RepAdmin
tags: [repadmin,kcc,replica,error]
---
As part of my Active Directory health checks,  I schedule a few command-line diagnostics and have them emailed to me on a regular basis for my perusal; I like to make sure that everything is always in tip-top shape.

This morning, looking through one of the logs, I noticed a couple of errors.

The report was the output from `repadmin /showrepl *` and here is a sample of the error which I received relating to two of our RODC's:

![1-2](/content/images/2018/07/1-2.JPG)


##The Solution
Although it looks drastic, the fix is actually quite easy:

I deleted the connection object in *Sites and Services* for the server in question and recreated it.

Running `repadmin /showrepl *` showed no errors for the same servers once I had [recreated the connection objects]({{ site.baseurl }}{% link _posts/2018-07-16-RODC-How-to-Create-a-New-Connection-Object.md %}) and allowed replication to take place.