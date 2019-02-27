---
layout: post
title:  "PowerShell: How to determine which DNS records are Tombstoned"
date:   2015-11-05 22:00:00 +0000
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