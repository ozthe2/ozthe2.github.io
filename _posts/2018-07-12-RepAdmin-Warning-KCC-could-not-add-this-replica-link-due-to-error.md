---
layout: post
title:  "REPADMIN: Warning: KCC could not add this REPLICA LINK due to error"
date:   2018-07-12 22:00:00 +0000
categories: RepAdmin
tags: [repadmin,kcc,replica,error]
---
As part of my Active Directory health checks,  I schedule a few command-line diagnostics and have them emailed to me on a regular basis for my perusal; I like to make sure that everything is always in tip-top shape.

This morning, looking through one of the logs, I noticed a couple of errors.

The report was the output from `repadmin /showrepl *` and here is a sample of the error which I received relating to two of our RODC's:

![1-2](/assets/images/1-2.JPG)


## The Solution
Although it looks drastic, the fix is actually quite easy:

I deleted the connection object in *Sites and Services* for the server in question and recreated it.

Running `repadmin /showrepl *` showed no errors for the same servers once I had [recreated the connection objects]({{ site.baseurl }}{% link _posts/2018-07-16-RODC-How-to-Create-a-New-Connection-Object.md %}) and allowed replication to take place.

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)