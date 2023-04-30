---
layout: post
title:  "USMT: Backup Google Chrome Bookmarks"
date:   2016-03-11 22:00:00 +0000
categories: USMT
tags: [usmt, backup, bookmarks, google, chrome]
---
I needed to backup bookmarks from the Chrome web browser using USMT as part of an image refresh task I’ve recently implemented using SCCM 2012R2 + MDT Integration.

Searching the Internet (why re-invent the wheel eh?) only gave me a couple of results, and when trying the ‘solution’ I found that it did not work.

Here is the main post that I used as a reference: http://www.itninja.com/question/user-state-migration-tool-1

The reason it failed was that the detection rule path in *migapp.xml* (referred to in the above link) was failing. When I installed Chrome on my system, the registry key ```HKLM\SOFTWARE\Wow6432Node\Google\Chrome``` that is being detected did not exist:

![g1](/assets/images/g1.PNG)

I shortened the path of the detection rule to: 

```HKLM\SOFTWARE\Wow6432Node\Google``` which was the only path that existed in my test systems and that did the trick.

So all you need to do is modify *migapp.xml*…

This is the original, remove the two existing detection rules (highlighted in yellow):
![g2](/assets/images/g2.PNG)

…and replace them with the single new detection rule:
![g3](/assets/images/g3.PNG)

To save you typing, copy and paste this into your *migapp.xml*:

```xml
<condition>MigXmlHelper.DoesObjectExist("Registry","%HklmWowSoftware%\Google\")</condition>
```

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)