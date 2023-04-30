---
layout: post
title:  "PowerShell: Get Multiple IP Address, Subnet, DNS, MAC and more"
date:   2017-10-05 22:00:00 +0000
categories: PowerShell
tags: [powershell, posh]
---
Isn’t it funny that the ‘Hello World’ of PowerShell, the Great Grand-Daddy of ‘here’s a real world example’ found in online tutorials and books everywhere happened to be just the thing that we actually needed at work today.

We have many servers in over 30 countries and sometimes you need to very quickly get disk info, or IP info or..you get the idea.  Well, today was the straw that broke the camels back as they say and I decided to write my own ‘Hello World!’  One of the requirements we had was to report multiple IP addresses \ network info which this script does.

Its very imaginatively entitled, *Get-OHComputerInfo*

You can also pipe to it; great for 
```Get-ADComputer | Get-OHComputerInfo``` type fun.  Try piping it to ```Export-CSV``` or ```Out-Gridview``` for a quick and crude method of documenting your servers!

I've put the whole thing in a module called *OHTools* as I can then add other 'tools' to it as and when I get around to it.  It's currently on version 1.4 and has 100% code coverage with Pester - although there's certainly room for more tests!

[https://github.com/ozthe2/OHTools](https://github.com/ozthe2/OHTools)

[![Build status](https://ci.appveyor.com/api/projects/status/aonepjox78v7xhff?svg=true)](https://ci.appveyor.com/project/ozthe2/ohtools)  

It is also in the [PowerShell gallery](https://www.powershellgallery.com/packages/OHTools/1.3) so if you have PowerShell 5 you can install by simply typing: 

```powershell
install-module ohtools
```

and update to newer releases with:
```powershell
update-module ohtools
```

To see the available cmdlets and version number:
```powershell
get-command -module ohtools

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)