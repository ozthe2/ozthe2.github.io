---
layout: post
title:  "Direct Access: Unable to Add a New Entry Point"
date:   2018-09-27 22:00:00 +0000
categories: DirectAccess
tags: [directaccess]
---
"The cmdlet did not run as expected." Zoiks!  Here's how I fixed it...

### The Issue:
I was trying to add a new entry point to our Direct Access Multi-Site configuration and it failed with the error "The cmdlet did not run as expected."
I also had a warning informing me that the DNS entry for the web probe could not be created and it should be created manually. (I think this warning was unrelated to the main issue of the entry point installation failing.)

![](/assets/images/DAEntryPointErr.png)

### The Solution:
Our organisational Direct Access infrastructure was built on Microsoft Server 2012 R2.  
When I built the new Entry Point server in our Dubai office I used Microsoft Server 2016.  This was why it failed as you cannot mix operating systems.
Bizarre, I know.
So I rebuilt the Entry Point server, this time using Microsoft Server 2012 R2, the same as all of our other DA and Entry point servers, ran the 'Add Entry Point' wizard again and bingo!  It worked.

---

**Get my book:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)