---
layout: post
title:  "ConfigMgr: How to Use Powershell to Only Keep the Most Recent X Backups of Cd.Latest"
date:   2017-01-05 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, powershell, backup]
---
If like me, you followed [Kent Agurlund's excellent guide on how to create SCCM backups using SQL](http://blog.coretech.dk/kea/configuring-backup-in-configmgr-current-branch/) you will have noticed that while it will only keep the last 7 backups, when you come to configure the cd.latest backups as an additional SQL job this will roll on forever, eventually consuming all of your precious disk space.

In order to match it up with the main SQL backup, I used Powershell to delete any of the cd.latest backups that are over 7 days old which I run as a scheduled task.

(Like a lot of Powershell tasks, the actual code to achieve it is actually just one line, padded out by making it a reusable function with parameters.  This means you could also replace the parameters in that single line of PowerShell within my function with hard-coded values and incorporate it directly into the PowerShell that creates the archive.zip files in the first place in the SQL job as per Kent's post.  Simply separate it from the other code with a semi-colon)

Following his guide, all of my CD.Latest backups are .zip files named archive\<dateTime>.zip and the powershell script additionally will only delete files that are zip files and have the word 'archive' in the file name.  This is a parameter of the function and you can change this from the default of 'archive' to anything you like as well as deleting files over x days old instead of the default 7.

To schedule the task, ensure that the account you run the task as has permissions to delete the files in the location you specify in the path parameter.

Schedule the task with the program: powershell.exe and the arguments similar to this:

```powershell
-ExecutionPolicy unrestricted -command "& { . c:\delete-filesolderthan.ps1; delete-filesolderthan }"
```

(Add any parameters before the last curlybrace eg *-path c:\my\path"}*)

And of course you can always add *-whatif* to test before you commit ;-)

Find the script [here](https://github.com/ozthe2/Powershell/blob/master/CF/Delete-FilesOlderThan).