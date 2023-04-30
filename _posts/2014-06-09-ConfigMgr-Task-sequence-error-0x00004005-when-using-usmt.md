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

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)