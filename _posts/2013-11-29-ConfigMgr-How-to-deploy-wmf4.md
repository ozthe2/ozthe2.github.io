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