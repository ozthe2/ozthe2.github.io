---
layout: post
title:  "ConfigMgr: How to Deploy Windows Management Framework 4.0"
date:   2013-11-29 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, wmf]
---

If you want to know how I deployed WMF 4.0 then you will want to read this post.

WMF 4.0 requires the .Net 4.5.x framework as a pre-requisite.   Two reboots are required: the .net framework will require a reboot and the WMF will require a reboot.

I chose to make the .net framework a dependency of the WMF 4.0 deployment and to suppress all reboots.  The deployment will then install .Net 4.5.1 and wait until the next reboot when it will then continue to deploy WMF 4.0 which will also wait for a reboot.

Here's how I did it:

1. Create the .Net 4.5.1 application.  To do this, see my step-by-step guide [here]({{ site.baseurl }}{% link _posts/2013-11-28-ConfigMgr-How-to-deploy-dotNet-Framework.md %}).

2. Create the WMF 4.0 application.  To do this, refer to my step-by-step guide here on deploying WMF 3.0 [here]({{ site.baseurl }}{% link _posts/2013-11-15-ConfigMgr-How-to-deploy-wmf3.md %}), but make the following changes to the guide: 

- Download WMF 4.0 instead of WMF 3 obviously!

- Change all references in the application to the name Windows Management Framework 3.0 to Windows Management Framework 4.0 (Again - obvious!)

-  Change step 10 in the WMF 3.0 installation guide:

The detection method should now detect version 6.3  of the powershell executable as shown below: (The actual full version number is 6.3.9600.16406)

![WMF4DetectionRule](/assets/images/wmf4/WMF4DetectionRule.png)

- Change step 15 in the WMF 3.0 installation guide:

Add the .net framework 4.5.1 as a dependency of the WMF 4.0 application:

![Dependency](/assets/images/wmf4/WMF4Deps.png)

Then deploy only the WMF 4.0 Framework application.

Once deployed successfully, the powershell version can be confirmed by opening a powershell window and typing ```$psversiontable``` at the prompt:

![Powershell version](/assets/images/wmf4/Powershell-v4.png)

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)