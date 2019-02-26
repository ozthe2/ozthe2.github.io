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