---
layout: post
title:  "Failover Cluster: Error 0x800703eb when creating File Server role"
date:   2018-09-16 22:00:00 +0000
categories: FailoverCluster
tags: [failovercluster, cluster, 0x800703eb]
---
Having created a new cluster today I received the following error when trying to configure the File Server role:
*Cannot complete this function. Ox800703eb*

![](/assets/images/ErrorCreatingFileServerRole.png)

## The Solution:
I had forgotten to give the Cluster Name Object (CNO) the permissions it requires in Active Directory.

On the OU that contains your cluster Server nodes \ CNO perform the following steps:
- Right-click the OU -> Properties -> Security -> Advanced
- Change the object type to 'Computer' and select your CNO. 
- Grant it the following permissions: 'Create Computer Object' and 'Read All Properties'
- Then delete the role from cluster manager and re-add it.

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)