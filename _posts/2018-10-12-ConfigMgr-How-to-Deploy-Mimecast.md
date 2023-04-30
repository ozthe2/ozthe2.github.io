---
layout: post
title:  "ConfigMgr: How to Deploy Mimecast using PowerShell"
date:   2018-10-12 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr,powershell,deployment]
---
If you want to know how I deployed the Mimecast plugin using ConfigMgr and PowerShell then you will want to read this post...

Today I had to make the new Mimecast for Outlook plugin available in the Application Catalogue.

I haven't deployed this in a while and the last time I did so it was via the conventional 'Application' method.
Since then however, I now deploy new applications using PowerShell scripts as it gives me greater flexibility and control.  It's also significantly faster and more pain-free for those apps that need frequent updating. (Java - I'm talking about you!)

The Mimecast for Outlook plugin requires that Outlook is closed and the correct version (32 bit or 64 bit) of the msi is installed depending on the bitness of Outlook. ie a 64 bit installation of Office versus a 32 bit installation of office.
(
    The majority of our users have 32 bit installations of office, however, we have a few exceptions.)
As the previous version of this application was not deployed using a PowerShell script, it was time to migrate it...

The script  [Install-Mimecast.ps1](https://github.com/ozthe2/Powershell/blob/master/SCCM/Install-Mimecast.ps1)  is in my GitHub repository and all you need to do is ensure that the .ps1 script and both Mimecast msi files (x86 and x64) are present in the same source directory on your Config Manager server and then deploy the Powershell Script using the SCCM Application method, selecting whatever detection method and other criteria that meets your needs.

The script will automatically close Outlook if it's open, which would otherwise prevent a successful installation and also checks for the Office bitness in order to install the correct msi version of Mimecast.

At the end of the day, it's a PowerShell script so if you want to enhance it, the sky's the limit.  Want to add a notification to the user if Outlook is open?  Go for it!  Want some logging?  Go for it! Want it to make a cup of tea after script execution? Go for it!  
If you don't already deploy your applications via PowerShell, now's the time to get into the habit - in the long run, you will thank yourself for it.
NB: If you're not sure how to go about deploying a PowerShell script, I will cover this step-by-step in my next post coming soon, using Mimecast as a 'real-world' example.

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)


"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)