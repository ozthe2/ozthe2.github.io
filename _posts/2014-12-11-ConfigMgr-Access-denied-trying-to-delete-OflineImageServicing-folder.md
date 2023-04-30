---
layout: post
title:  "ConfigMgr: Access Denied Trying to Delete OfflineImageServicing Folder"
date:   2014-12-11 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, dism]
---

ConfigMgr - If you are trying unsuccessfully to delete the OfflineImageServicing folder then you will want to read this.

Last week I tried to incorporate some updates into our image. (Right-click the image -> Schedule Updates) Unfortunately the process failed (That’s a story for another post!) and left a temporary directory behind that had around 8Gb+ of files behind.  This was space that I needed to claw back!  The temporary directory used is the staging directory and can be found in the root drive of your CCM installation in a folder called: *ConfigMgrOfflineImageServicing*

When you try and manually delete this, you are presented with the following error:
![1-1](/assets/images/1-1.JPG)

If like me, you may have thought that taking ownership of the directory and sub-dirs will then enable you to delete it.  Well then think again!  Because you still can’t!  Restarting the server will also not help.

CCM mounts a copy of the image temporarily in this directory, and using DISM I was able to clearly see that this was still mounted and in an error state with a status shown as invalid.

I ran the following command to see this info:
`dism /getMountedWimInfo`

![2-1](/assets/images/2-1.JPG)

I then tried to un-mount it using the following command:

```dism /unmount-wim /mountdir:c:\ConfigMgr_OfflineImageServicing\XXXXXX\ImageMountDir / commit```

That failed:

![3-1](/assets/images/3-1.JPG)

I then thought I’d better look up the documentation for this command as it’s been a while since I’ve used it.  I looked [here](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-7/dd744382(v=ws.10)), and found the answer:

`dism /cleanup-wim`

I’ll leave you to read the document for this command yourself.  Suffice to say, it did the job!  Disk space reclaimed!

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)