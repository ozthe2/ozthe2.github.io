---
layout: post
title:  "ConfigMgr: How to Read & Write Custom Vars Using PowerShell in a Task Sequence"
date:   2014-10-22 18:00:00 +0000
categories: ConfigMgr
tags: [configmgr, tasksequence, powershell, posh]
---

If you want to know how to read and write custom variables in a SCCM task sequence then you will want to read this. (Part 1 of 2)

I’ve been looking for a method of reading and writing custom variables from within a task sequence as I will shortly be writing a Powershell GUI front-end for our imaging task and being able to do this step is an essential pre-requisite to achieving my end goal.

I used three Microsoft articles in my research on how to do this:
1. [About Task Sequence Variables](https://technet.microsoft.com/en-us/library/bb693541.aspx)
2. [Task Sequence Built-In Variables](https://technet.microsoft.com/en-us/library/bb632442.aspx)
3. [Prestart commands for task sequence media](https://docs.microsoft.com/en-us/previous-versions/system-center/system-center-2012-R2/jj651034(v=technet.10))

I thought I would try a ‘real-world’ example – something that may have some real value in the workplace –  while I tried to figure out how all of this worked.  I decided to use the tried and tested “Hello World!” SCCM equivalent of logging the following information into the computers registry once imaging was complete :

* Date image started
* Image Start time
* Image End Time
* Total time taken to image
* Task sequence used to image
* Name of image used

Here is a screenshot of the final result taken from the registry of an imaged computer:

![1-1](/assets/images/TSLogging/9.JPG)

[Part 2]({{ site.baseurl }}{% link _posts/2014-10-22-ConfigMgr-Logging-the-time-taken-to-run-a-task-sequence.md %}) explains how I went about achieving this.

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)