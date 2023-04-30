---
layout: post
title:  "PowerShell: How to determine which DNS records are Tombstoned"
date:   2014-11-05 22:00:00 +0000
categories: PowerShell
tags: [powershell, posh, dns. tombstone]
---
If you want to find out how I used PowerShell to determine which DNS records have been tombstoned then you will want to read this post.

Today, I had cause to find out which DNS records had been tombstoned and naturally my thoughts of a solution turned to using PowerShell.  

Seeing as I couldn’t find this info on the ‘Googles’ I decided to figure it out myself and thought it may come in handy for someone else.

Here’s the basic line that you can tailor to meet your needs , obviously you will need to edit  the searchbase to use your domain in place of my ‘*DC=oh,DC=Pri*’:

```powershell
Get-ADObject -filter 'dnsTombstoned -eq $true' -SearchBase 'dc=oh.pri,CN=MicrosoftDNS,DC=DomainDNSZones,DC=oh,DC=Pri' -Properties  dNSTombstoned,name,distinguishedName,whenchanged
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