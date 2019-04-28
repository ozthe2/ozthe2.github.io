---
layout: post
title:  "ConfigMgr: Task sequence error 0x00004005 when using USMT"
date:   2014-06-09 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, tasksequence, usmt]
---

If you are using USMT in your SCCM task sequence and receive error 0x00004005 when it requests the state store, then you will want to read this.

Here’s a strange one that took me a while to figure out.  I was incorporating USMT into a new task sequence and it kept failing right at the start of the USMT section: ‘Request State Store’ where it would hang for a couple of minutes until it timed out and presented me with the error: 0x00004005

![1-8](/assets/images/1-8.PNG)

I checked the *smsts.log* on the client computer and could see where it had tried the computer account and failed on credentials (as expected), and then said that it was about to try the Network Access account.  When it did so, it showed the error: ‘Cannot connect to *http//servername SMP root share.*‘  No mention of credentials being wrong.

What’s more, to contradict that error, I could manually connect to the SMP share that the log was whining about using the Network Access Account.

I had tried resetting the Network Access account password, removing the SMP role and adding it back, rebooting the server and the perusal of several log files as well as trying drastic things out such as giving excessive permissions to the Network access account just to rule it out.  Even Google couldn’t help me.

The solution – and it took a while for me to figure this one out, was that I was trying this all out in Hyper-V.  It suddenly dawned on me that I had not tried to run the task sequence on a real ie physical computer and as soon as I did –  bingo!  Success!

---

**Get my book:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)