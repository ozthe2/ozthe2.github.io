---
layout: post
title:  "ConfigMgr: PXE Error 0xc000000f"
date:   2013-06-03 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, pxe]
---

If you get PXE Error 0xc000000f then have a read of this as it may be the solution you have been looking for.

Here’s a good one:  Today I came in to work only to be told that imaging had stopped working.  When trying to PXE the computer would display the error of 0xc000000f and went on about Windows failed to start. File: \Boot\BCD 

Here’s a screenshot of the actual error:

![1-9](/assets/images/1-9.PNG)

The first place I checked was the SMSPXE.log which is on the Config Manager server itself and can be found in the following location:  C:\Program Files\SMS_CCM\Logs

The log didn’t help me out too much other than showing me a log full of errors.  An Internet search revealed nothing of value either.  Here’s what the log looked like:

![2-8](/assets/images/2-8.PNG)

My next port of call was checking the site system components in the Configuration Manager 2012 Administration console. (Select ‘Monitoring’ at the bottom left-hand column in the console, then expand ‘System Status’ and click on ‘Component Status’)  When I did this I saw the following:

![3-7](/assets/images/3-7.PNG) 

I then right-clicked SMS_MP_CONTROL_MANAGER that was shown to be in a critical condition, then from the pop-up menu selected ‘Show Messages -> Warning’ for the period ‘1 day ago.’

I was then presented with hundreds of the following warnings:

![4-7](/assets/images/4-7.PNG) 

Now I was getting somewhere:  The description told me that the ‘MP has rejected the request because…certificate had expired‘

I then went to the properties page of our distribution point…

![5-7](/assets/images/5-7.PNG) 

… where the problem stared at me in the face:

![6-6](/assets/images/6-6.PNG) 

We use a self-signed certificate and it had expired!

#### The solution:
I changed the expiration date of the self-signed certificate to a future date and restarted the config manager server.  (*Note:* the restart is required)

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)