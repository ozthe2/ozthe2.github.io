---
layout: post
title:  "Server2012R2: Net.Pipe and Net.Tcp Service Not Starting After In-Place Upgrade to Server 2012R2"
date:   2015-03-04 22:00:00 +0000
categories: Server2012R2
tags: [server2012, Server2012r2, server2008, server2008r2, upgrade]
---
Having just performed an in-place upgrade from Server 2008R2 to 2012R2 on two of our DHCP servers, I noticed the following two errors in Server Manager once the upgrade was complete:

![1-5](/assets/images/1-5.PNG)

When Clicking on the Services link I was presented with the information that Net.Tcp Listener Adapter and the Net.Pipe Listener Adapter services could not be started.

When I checked the services it could clearly be seen that they were set to automatic but had not started.  Manually trying to start the services would not work either.

![2-4](/assets/images/2-4.PNG)

The solution was in two parts.  The first was to fully patch the server – on checking I found the server had 41 updates required.

Once I had patched and restarted the server, I only had one error in Server Manager:

![a](/assets/images/a.PNG)

The only error now was showing that the Net.Tcp Listener Adapter service was in a stopped status:

![b](/assets/images/b.PNG)

When I tried to start it manually I received the following error:

![3-4](/assets/images/3-4.PNG)

I checked the Event log and found the following information:

![4-4](/assets/images/4-4.PNG)

Cool – now we’re getting somewhere.. I needed to start the Net.Tcp Port Sharing Service.  When I checked, it was indeed disabled.
I set it to automatic:

![5-4](/assets/images/5-4.PNG)

Once that was done, I attempted to start the Net.Tcp Listener Adapter service again:

![6-3](/assets/images/6-3.PNG)

Success!

![7-3](/assets/images/7-3.PNG)


---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)