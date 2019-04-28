---
layout: post
title:  "Azure Backup Server: Not Backing Up to Azure on New Install"
date:   2018-05-13 22:00:00 +0000
categories: AzureBackupServer
tags: [azurebackupserver]
---
I have just installed Microsoft Azure Backup Server and in the process of testing discovered that it was not backing up to Azure.

On checking the error log file, CBEngineCurr.errlog, found at *C:\Program Files\Microsoft Azure Backup Server\DPM\MARS\Microsoft Azure Recovery Services Agent\Temp* I saw that there were errors relating to the scratch location.  On closer inspection, I saw that it could not access a custom path that I had changed when I installed the program initially.

When I installed the program, I changed the scratch location path as well as the Staging Area location; I noticed at the time that the installer presented the custom path with a double backslash but thought nothing of it, assuming this was just how the information was presented. (See screenshots below)

![1-1](/assets/images/1-1.PNG)

![2-1](/assets/images/2-1.PNG)

### The Solution
To start with, I edited the scratch path and removed the extraneous backslash so that it now reflected the proper path.  To do this, I had to use Regedit and make the adjustment in 2 places:


> ##### HKLM\Software\Microsoft\Microsoft Azure Backup\Config

> ##### HKLM\Software\Microsoft\Microsoft Azure Backup\Config\CloudBackupProvider

and edit the ScratchLocation value in both locations.

The next step was to edit the Staging area location.  I did this from within the Backup Server Management console ->Management -> Online -> Configure:

![3-1](/assets/images/3-1.PNG)

And under ‘Recovery Folder Settings’ is where I made the change.  Then you need to follow the wizard through next, next etc to the end in order to save your changes.

Staging Area Before:
![4-1](/assets/images/4-1.PNG)

Staging Area After:
![5-1](/assets/images/5-1.PNG)

To finish off, I restarted the server and continued my testing.  Azure backup worked as expected and the error logs were error free.

---

**Get my book:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)