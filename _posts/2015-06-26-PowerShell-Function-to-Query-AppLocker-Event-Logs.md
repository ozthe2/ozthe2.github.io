﻿---
layout: post
title:  "PowerShell: Function to query AppLocker event Logs"
date:   2015-06-26 22:00:00 +0000
categories: PowerShell
tags: [powershell, posh, applocker, eventlogs]
---
If you want to know how I queried AppLocker event logs using PowerShell then you will want to read this post.

I have configured AppLocker to run in ‘Audit’ mode and wanted a quick method of seeing what would be blocked without having to log on to individual computers and checking the event logs.

That way I can pro-actively monitor computers and build the white-list rules before I turn AppLocker on to ‘Enforce’ mode.

I’ve seen there are a number of AppLocker cmdlets that I’ll be exploring later, but for now, [here’s my solution on GitHub](https://github.com/ozthe2/Powershell/blob/master/Tools/Get-ApplockerBlocks).

---

**Get my book:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)