---
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

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)