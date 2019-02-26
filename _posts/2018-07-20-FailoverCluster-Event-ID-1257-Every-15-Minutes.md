---
layout: post
title:  "Failover Cluster -  Event ID 1257 every 15 minutes"
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

###The reason:
*Before* creating the cluster, I had pre-added the DNS 'A' record for the CNO that I would need using IPAM.

###The solution:
I simply deleted the CNO 'A' record in DNS and recreated it, ensuring that when I did so, I ticked, "*Allow any authenticated user to update DNS record with the same owner name*"

If you do not pre-create the CNO A record in DNS then you will not have this issue.