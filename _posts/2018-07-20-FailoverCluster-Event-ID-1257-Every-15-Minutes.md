---
layout: post
title:  "Failover Cluster: Event ID 1257 every 15 minutes"
date:   2018-07-20 22:00:00 +0000
categories: FailoverCluster
tags: [failovercluster, cluster, 1257]
---

Having just created a new cluster, I noticed Event ID 1257 being logged in the Cluster Events node within Failover Cluster Manager.

```
Cluster network name resource failed registration of one or more associated DNS name(s) because the access to update the secure DNS zone was denied.

cluster Network name: 'Cluster Name'
DNS Zone: *dns zone*

Ensure that cluster name object (CNO) is granted permissions to Secure DNS Zone.
```

Here's a screenshot of the actual events:
![ClustErr-1257](/assets/images/ClustErr-1257.png)

### The reason:
*Before* creating the cluster, I had pre-added the DNS 'A' record for the CNO that I would need using IPAM.

### The solution:
I simply deleted the CNO 'A' record in DNS and recreated it, ensuring that when I did so, I ticked, "*Allow any authenticated user to update DNS record with the same owner name*"

If you do not pre-create the CNO A record in DNS then you will not have this issue.

---

**Get my books:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)

---

"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)