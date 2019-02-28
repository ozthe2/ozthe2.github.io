---
layout: post
title:  "ConfigMgr: OSD Task Sequence Fails with Error 0x80091007"
date:   2012-11-09 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, tasksequence]
---

SCCM imaging failed with error 0x80091007 at the point of applying the operating system. Here's is how I fixed it.

After imaging a few computers recently, two of them failed at the point in the task sequence where it was going to apply the operating system.  The error displayed was 0x80091007 which appears to be a generic error.

Rebooting the computer gives the (somewhat expected) message of ‘Bootmgr is missing’

I checked SMSTS.log on the local computer that had the error and the following information was shown…

![1-3](/assets/images/1-3.PNG)

### The solution:
Changing the memory on the computer fixed the issue.