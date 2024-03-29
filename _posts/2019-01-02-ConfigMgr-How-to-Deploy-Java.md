﻿---
layout: post
title:  "ConfigMgr: How to Deploy Java using PowerShell"
date:   2019-01-02 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr,powershell,deployment]
---
If you want to know how I deployed Java using ConfigMgr and PowerShell then you will want to read this post...

In my [last podcast]({{ site.baseurl }}{% link _posts/2018-12-16-Podcast-Episode7.md %}) I spoke about a PowerShell script that I wrote that uninstalls all instances that it can find of msiexec installed applications.   I called this script Invoke-ApplicationRemoval and you can find it in my [Github repo here.](https://github.com/ozthe2/Powershell/blob/master/SCCM/Invoke-ApplicationRemoval)

In the same podcast, I also opined the virtues of using PowerShell to deploy applications using Config Manager.

Today I wanted to remove all installed versions of Java and then install both the 32bit and 64bit versions of the latest Java version using ConfigMgr.

To do this, I used my Invoke-ApplicationRemoval script with extra added sauce to install both versions of Java as well.  [You can find the script here.](https://github.com/ozthe2/Powershell/blob/master/SCCM/JavaVersionManagement.ps1) It's called *JavaVersionManagement.ps1*. 

All you need to do is to create a new Application in ConfigMgr and choose to make it of type: Script Installer.  
Then, for the Installation Program field in ConfigMgr use the following:

{% highlight powershell %}
powershell.exe -executionpolicy bypass -file .\JavaVersionManagement.ps1
{% endhighlight %}

![](/assets/images/javainstall.png)

And season with whatever detection rule you wish to use.  I normally use the Java.exe version number.  In my case I detect both the 32 and 64 bit versions of Java.exe to signify a successful deployment:

![](/assets/images/JavaVersionDetection.png)

Ensure that you place the .ps1 and your extracted msi java file(s) in the same directory where you normally store your ConfigMgr source files.

The only modification you need to make to the script is the name of the msi files on lines 101 and 102.  If you are only installing one version of Java, simply comment one of those lines out.

Once that's done, deploy to your computers and sit back as all current versions of Java are swiftly removed and your new version installed. (And how easy is this as a repeatable deployment when the next Java version comes out, eh? Suh-weet!)

I'm assuming a few things here:
- You know how to extract the Java msi file from the downloaded offline exe installer.
- You know how to create an Application of type Script Installer in ConfigMgr.
- You know how to deploy an application.

If you need me to explain any of this in more detail, please let me know via comments below or twitter: @ozthe2

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)