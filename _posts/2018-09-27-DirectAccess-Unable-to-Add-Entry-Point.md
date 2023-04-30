---
layout: post
title:  "Direct Access: Unable to Add a New Entry Point"
date:   2018-09-27 22:00:00 +0000
categories: DirectAccess
tags: [directaccess]
---
"The cmdlet did not run as expected." Zoiks!  Here's how I fixed it...

### The Issue:
I was trying to add a new entry point to our Direct Access Multi-Site configuration and it failed with the error "The cmdlet did not run as expected."
I also had a warning informing me that the DNS entry for the web probe could not be created and it should be created manually. (I think this warning was unrelated to the main issue of the entry point installation failing.)

![](/assets/images/DAEntryPointErr.png)

### The Solution:
Our organisational Direct Access infrastructure was built on Microsoft Server 2012 R2.  
When I built the new Entry Point server in our Dubai office I used Microsoft Server 2016.  This was why it failed as you cannot mix operating systems.
Bizarre, I know.
So I rebuilt the Entry Point server, this time using Microsoft Server 2012 R2, the same as all of our other DA and Entry point servers, ran the 'Add Entry Point' wizard again and bingo!  It worked.

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)