---
layout: post
title:  "Azure Backup Server: Unable to Save Backup Policy"
date:   2017-05-11 22:00:00 +0000
categories: AzureBackupServer
tags: [azurebackupserver]
---
I discovered today that Azure Backup has a maximum number of exclusions that can be included when configuring your backup policy.

Once you go over 90 exclusions, you are presented with the following error:
> The backup policy could not be modified.
> Error: Unable to save backup policy.  Selected items list for backup is large or
> selected items have long path names or selected large number of retention choices.  Please retry operation again after reducing individual items (selecting complete folders can help) or reducing retention choices.

Note the File Exclusions count in the image below equals 91, triggering the error.
![AzBk1](/assets/images/AzBk1.PNG)

![AzBk2](/assets/images/AzBk2.PNG)

### Solution:
Reduce the exclusions list to 90 or below.

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)