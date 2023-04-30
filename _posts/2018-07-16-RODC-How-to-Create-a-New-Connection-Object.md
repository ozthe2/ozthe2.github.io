---
layout: post
title:  "RODC: How to Create a New Connection Object"
date:   2018-07-16 22:00:00 +0000
categories: RODC
tags: [rodc,connection]
---
There may come a time whereby you will need to create a new connection object for your RODC's due to someone inadvertently deleting the existing one by mistake, or having to deliberately delete and recreate the connection object as in [my case]({{ site.baseurl }}{% link _posts/2018-07-12-RepAdmin-Warning-KCC-could-not-add-this-replica-link-due-to-error.md %}).

Connection objects for RODC's require a quick 'tweak' in order to get them to function correctly.  If you don't, then they won't work.

Basically, you create your connection object as per normal, giving it the name *RODC Connection (SYSVOL)* if you are doing this for server 2012 or higher, or name it *RODC Connection (FRS)* for server 2008r2.

Then right-click the connection object you just created -> properties and select the *Attribute Editor* tab and in the *Options* attribute, enter *0x40* for the value:
![1RODC](/assets/images/1RODC.JPG)

That's it.

You *know* I'm not clever enough to just know all this right?  Right?  

Yeah... I got this information from here: [Clever people](https://support.microsoft.com/en-gb/help/3212965/events-6804-and-2843-are-logged-and-rodcs-do-not-replicate-sysvol)

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)