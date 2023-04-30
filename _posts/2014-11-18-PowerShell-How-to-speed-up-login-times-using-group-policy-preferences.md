---
layout: post
title:  "PowerShell: How to speed up login times using Group Policy Preferences"
date:   2014-11-18 22:00:00 +0000
categories: PowerShell
tags: [powershell, posh, gpp, login, grouppolicy]
---

If you want to know how I significantly reduced login times using PowerShell and Group Policy then you will want to read this post.

If you're anything like me, Group Policy preferences revolutionised the way I achieved things.  They seemed to answer a lot of our prayers as Admins and simplified a lot of tasks that otherwise would have been painful and \ or convoluted to implement.

One of the changes I made at my workplace was to deploy our printers using the new Group Policy User Preference item: Printers

![1-1](/assets/images/1.JPG)

Once I had created a new 'Shared Printer' I then used the Targeting feature to ensure that it would only apply if the computer was in a certain Organisational Unit (OU):

![1-1](/assets/images/2.JPG)

I could then add multiple printers to the same Group Policy; I had one Group Policy object which I deployed to my 'Users' and through the clever use of 'targeting', the logged in computer was sure to only receive the printer deployment that it should.
The whole process was genius and our single GPO contained over 80 printer deployments \ deletions.
You gotta love GPP's!

I did,  until today.  Actually the story began last week when I was logging into a computer and thought that the process was incredibly slow.  I nailed the delay down to the printers being installed. (As they are installed on a user basis not computer; they are installed on every login.)
I decided to experiment with an alternative method of installing the printers and naturally I turned to Powershell to do this.  After getting some basic timings, I knew this was the way to go.
I wanted to achieve this with as little work as possible (don't we all?) and so over the weekend I started to devise a cunning plan....

Cue Monday morning....
I wrote a Powershell script that reads the XML of the GPO containing the GPP for the Printers and installs \ deletes the printers based on whatever's already there.
To clarify, I unlinked the existing GPO that deploys printers so it is in effect, just a 'placeholder' sitting there holding the printer info...which printer, who gets it, is it default etc and then read that info into a variable in my PS script - the variable is then parsed and printers deployed via the same script based on this information.

This has the added benefit of procedures remaining the same.  If someone already knows how to add a new printer deployment to the GPO, they continue exactly as they have always done.  Nothing has changed. (Except the GPO is no longer linked anywhere.)
I created a new GPO that simply deploys my Powershell script to users.

I wrote the script so that it is as generic as possible.  E.g. you do not need to specify a domain, or an OU etc etc the script will sort all of this out.  The only parameter you will need to supply is the GUID of your GPO that contains your printer GPP deployments.  To get that, simply select the 'Details' tab and copy the UniqueID (including the curly braces):

![1-1](/assets/images/3.JPG)

I should also point out that at the moment, the script will only work if you use GPP exactly as I have described.  ie. You deploy shared printers and you target computers belonging to specific OU's.

I will be actively working on this script so that  it also works with users in specific OU's as well as Users being members of security groups.  Alternatively, go ahead and make any mods yourself if you cannot be bothered to wait for me.

### How to use the script:

1. To use the script, you will need to change the very last line which is the entry point into the script - simply change the GUID that is currently there to the GUID that your GPO uses.
2. Once you've done that, UNLINK the current GPO that you use for deployments.
3. Deploy the Powershell script as a Logon script via a new GPO to your users:

![1-1](/assets/images/4.JPG)

![1-1](/assets/images/5.JPG)

### The Proof:
I found timings similar to these on all of the computers I tested.  None of the computers I tested had SSD's.
Using Standard GPP's:
Login1 (Profile created as never logged in before):  1:58 (Minutes: Seconds)Login2: 1:00Login3: 1:00
Using Powershell:
Login1 (Profile created as never logged in before):  1:02 (Minutes: Seconds)Login2: 0:17Login3: 0:17
That is not a typo!  Seventeen seconds reduced from over a minute!  When I tested this on some of our older computers that receive multiple printers I reduced the login time from 2 minutes 35 seconds to a staggering 25 seconds!

### Get the script:
You can find the script as it is so far [here](https://github.com/ozthe2/Powershell/blob/master/Active-Directory/DeployPrinters) in my Github repository.

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)