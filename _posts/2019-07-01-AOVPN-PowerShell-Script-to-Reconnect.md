---
layout: post
title:  "AOVPN: PowerShell Script to Reconnect."
date:   2019-07-01 19:00:00 +0000
categories: AOVPN
tags: [aovpn, always-on-vpn, powershell]
---

AOVPN doesn't always reconnect - here's how I remediated it.

Always On VPN is, let's face it, not all it's cracked up to be.  Even at this late stage in the game it has many issues and simply is not (in my opinion) as robust as Direct Access.

One issue our users have found is that if their Internet connection 'breaks' for any reason and AOVPN disconnects, say through a ropey Internet connection, waking up from sleep or hibernation or any other edge-case scenario that causes AOVPN to disconnect, then it's more than probable AOVPN will not auto-reconnect.  At least, not in any reasonable time.

Not really living up to it's name.

As usual, it falls to us lowly administrators to try and mitigate these issues as best as we can, and to that end, I wrote a Powershell script that tries to do just that.

The script is intended to be run as a Scheduled Task.  I have the task triggers set to event ID's such as waking from sleep \ hibernation, if the network connection drops then re-establishes etc etc. 

The script first checks to see if the disconnected device is on the corporate LAN, as if it is, I don't want the script to try and connect to AOVPN.

If the device is not on the corporate LAN and AOVPN is not connected, then try to connect a predetermined number of times before giving up.

The number of times it tries to reconnect is a configurable parameter that can also be set to ['never stop, never stopping'](https://en.wikipedia.org/wiki/Popstar:_Never_Stop_Never_Stopping) by  setting the *-ConnectionAttempts* parameter to 0.


### The Script:
[Start-AOVPN can be found in my GitHub repo here.](https://github.com/ozthe2/AOVPN/blob/master/Start-AOVPN)

The script has full comment-based help so make sure you have a read-through of it.



---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)