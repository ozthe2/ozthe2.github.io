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

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)