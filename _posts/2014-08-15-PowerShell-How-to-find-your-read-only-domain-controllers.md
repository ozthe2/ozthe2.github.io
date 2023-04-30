---
layout: post
title:  "PowerShell: How to Find Your Read-Only Domain Controllers (RODC)"
date:   2014-08-15 22:00:00 +0000
categories: PowerShell
tags: [powershell, posh, rodc]
---
If you want to know one method of finding your RODC's using PowerShell then you will want to read this.

TL;DR: `Get-ADDomainController -filter {isreadonly -eq $true}`

This week I introduced a 2012R2 Read Only Domain Controller (RODC) into our domain and I already have a couple of Powershell scripts in mind that I want to write in order to help manage this DC.

That said, I thought it would be a good idea to be able to identify the RODC’s in our domain via Powershell as a first step, as it’s likely we are going to add more RODC’s at some of our other remote sites.

So, here is how my thought process went:

### 1.
I thought I’d take a look at modules available by typing: 

```powershell
get-module -listavailable
```

![1](/assets/images/RODC/1.JPG)

Looking through the displayed list, it looked like I was probably going to find what I needed in the ActiveDirectory module.

### 2.
I then took a look at the available commands within that module to see if there were any specific RODC ones available.  I did this by typing: 
```powershell
get-command -module ActiveDirectory
```

![2](/assets/images/RODC/2.JPG)

Well, I didn’t really see anything specific to what I was looking for, however I did see a couple of commands that may come in useful later that look specific to RODC’s – namely the add and get-ADDomainControllerPasswordReplicationPolicy.

Well, an RODC is a domain controller, so let’s take a look at the Get-ADDomainController cmdlet…

### 3.
I started off by looking at the help for this cmdlet using: 
```powershell
help get-addomaincontroller -full
```

Reading the help file did not show me any specific RODC parameters, however, it did have a *-filter* parameter that I thought could come in handy.

### 4.
I now knew that I was probably going to use the Get-ADDomainController cmdlet with the filter parameter.  So to see if I could find anything relevant to filter on, I looked at the attributes of my RODC in Active Directory Users and Computers:

![3](/assets/images/RODC/3.JPG)

Well – maybe I missed it but I couldn’t see anything overly relevant that would identify a RODC that could be used in a filter. (Actually, I did notice the msDS-RevealedUsers attribute but I really wanted something very specific.)

I was determined not to ‘Google’ this, so for my next step….

### 5.
I piped *Get-ADDomainController* to *Get-Member* to see if that revealed anything useful and…

![5](/assets/images/RODC/5.JPG)

Bingo!  We have hit the jackpot!  An ‘*IsReadOnly*’ property.

### 6.
Now to try this out in a filter.  I tried the following command: Get-`ADDomainController -filter {isreadonly -eq $true}`

![6](/assets/images/RODC/6.JPG)

And we have success!

As mentioned above, I’m no expert and there may be a much more obvious method of achieving the same thing, but, this was my ‘non-google’ thought process.

I then started playing around with this property to query a 
specific DC to discover if it is a RODC by running this command: 

```powershell
(Get-ADDomainController -Identity servername).isreadonly
```
which returns true or false and opens up a few more scripting possibilities.  Brilliant!

![7](/assets/images/RODC/7.JPG)

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)