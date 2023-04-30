---
layout: post
title:  "ConfigMgr: Error 0x8007001A When Imaging with USMT in Task Sequence"
date:   2013-04-25 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, usmt]
---

If you want to know how I resolved SCCM error 0x8007001A when imaging with USMT then you will want to read this.

Our user support team encountered a new one today.  They were in the process of imaging an XP computer to Windows 7 and it failed right near the beginning of the USMT task sequence action:  ‘*Running Action: Capture User State*‘

![S1](/assets/images/S1.JPG) 

To get to the bottom of it, I pressed F8 on the computer in question and copied the *smsts.log* file onto a usb stick which I then looked at in the Configuration Manager Trace Log tool.  In there, highlighted nicely in red was the message: 
> USMT returned exit code (0x00000001a).  Look USMT log file scanstate.log for detail error message.”

![s2](/assets/images/s2.JPG) 

So I went back to the computer in question and then copied off *scanstate.log*. (The location of which could be found here:  *X:\WINDOWS\TEMP\SMSTSLog\scanstate.log*)  When I looked at this log, it showed a shed-load of error messages whilst trying to process a particular users profile.

![s3](/assets/images/s3.JPG) 

### The solution:
I booted the computer into Windows and manually backed up the user profile mentioned in the scanstate.log to usb storage and then deleted the profile from the computer.

I was then able to successfully image.

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)