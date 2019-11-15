---
layout: post
title:  "ConfigMgr: How To Deploy Language, keyboard and Regional Settings"
date:   2019-11-10 19:55:00 +0000
categories: ConfigMgr
tags: [configmgr, powershell, book, TS, task, sequence]
---

How to deploy language, keyboard and other regional settings using a native task sequence in ConfigMgr (SCCM) the easy way.

Did I say it was easy?  yup - it is.

I recently broke away from using an MDT integrated task sequence and now I use a nice and simple native task sequence for my OS deployments.

Life is much sweeter, especially now that I have broken down larger tasks into their own child task sequences.  Everything is just so neat and squishy now.

One hurdle I had to overcome though was deploying display language, keyboard and other regional settings without the very helpful MDT steps that were no longer available to me.

I'm very much into book writing and the solution can be found in my second book published on Leanpub:

[ConfigMgr - An Administrator's Guide to Deploying Language and Regional Settings](https://leanpub.com/configmgr-DeployLang/)

Let me save you hours and hours and hours of research, more research, testing, failure, testing, more testing and potentially giving up and going back to MDT.

Help me, help you help them.

![](/assets/images/smalllangbook.png)

---

If you want to obtain a great understanding of deploying pretty much anything using PowerShell and SCCM then you'll want to grab a copy of my book now.

[Get the book here](https://leanpub.com/configmgr-DeployUsingPS)
