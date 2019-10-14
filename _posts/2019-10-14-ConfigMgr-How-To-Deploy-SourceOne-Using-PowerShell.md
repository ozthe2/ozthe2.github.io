---
layout: post
title:  "ConfigMgr: How To Deploy EMC SourceOne using PowerShell"
date:   2019-10-14 20:00:00 +0000
categories: ConfigMgr
tags: [configmgr, powershell, book,emc,sourceone]
---

Last week I had to deploy a new version of the EMC SourceOne client for Offline files.

When I went to download the latest version, I discovered that I would need to deploy two setup.exe's: *Version 7.2 SP7* followed by *version 7.2 SP7 Hotfix 1.*

I deploy nearly all of my applications using PowerShell these days and this was no exception.

I used my deployment template as documented in my book, [ConfigMgr - An Administrator's Guide to Deploying Applications Using PowerShell](https://leanpub.com/configmgr-DeployUsingPS) which made what could have been a complicated, time-consuming  deployment into something that was simple, rapid and proven.

You have to install the appropriate version of SourceOne depending on the Office "bitness" and all of the code for doing this was built right in to the deployment template already - great stuff!

I've put the deployment code and the PowerShell detection rules in my [GitHub repo here](https://github.com/ozthe2/Powershell/tree/master/SCCM/SourceOne) so you can use it straight away in your own deployments.

If you want to obtain a great understanding of deploying pretty much anything using PowerShell and SCCM then you'll want to grab a copy of my book now.

[Get the book here](https://leanpub.com/configmgr-DeployUsingPS)
