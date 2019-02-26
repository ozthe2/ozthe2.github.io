---
layout: post
title:  "Failover Cluster - Error 0x800703eb when creating File Server role"
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