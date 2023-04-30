---
layout: post
title:  "ConfigMgr: How To Deploy EMC SourceOne using PowerShell"
date:   2019-10-14 20:00:00 +0000
categories: ConfigMgr
tags: [configmgr, powershell, book,emc,sourceone]
---

If you want to know how I deployed EMC SourceOne for Offline Files using PowerShell and SCCM then you will want to read this post.

Last week I had to deploy a new version of the EMC SourceOne client for Offline files.

When I went to download the latest version, I discovered that I would need to deploy two setup.exe's: *Version 7.2 SP7* followed by *version 7.2 SP7 Hotfix 1.*

I deploy nearly all of my applications using PowerShell these days and this was no exception.

I used my deployment template as documented in my book, [ConfigMgr - An Administrator's Guide to Deploying Applications Using PowerShell](https://leanpub.com/configmgr-DeployUsingPS) which made what could have been a complicated, time-consuming  deployment into something that was simple, rapid and proven.

You have to install the appropriate version of SourceOne depending on the Office "bitness" and all of the code for doing this was built right in to the deployment template already - great stuff!

I've put the deployment code and the PowerShell detection rules in my [GitHub repo here](https://github.com/ozthe2/Powershell/tree/master/SCCM/SourceOne) so you can use it straight away in your own deployments.

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)