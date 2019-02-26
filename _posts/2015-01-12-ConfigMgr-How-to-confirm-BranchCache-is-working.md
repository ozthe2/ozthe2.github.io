---
layout: post
title:  "ConfigMgr: How to Confirm BranchCache is Working"
date:   2015-01-12 22:00:00 +0000
categories: ConfigMgr
tags: [branchcache,configmgr]
---

This is part 2 of a two part post.  In [Part 1]({{ site.baseurl }}{% link _posts/2015-01-09-ConfigMgr-How-to-Configure-BranchCache.md %}) I explained how I configured BranchCache on my SCCM distribution point.

This post will demonstrate the methods I used to prove that computers at my branch office were actually using a locally cached version of the application to install from.

### 1.
Choose a computer in your branch office that you wish to test will be pulling the content from another computers local cache:
Either open Performance Monitor (type perfmon in the Run menu) directly on that computer or run it on your administration computer and right-click the Performance node and select ‘Connect to another computer’
![1-7](/assets/images/1-7.PNG)

### 2.
Expand the ‘Data Collector Sets’ node and right-click ‘User Defined’ -> New -> Data Collector Set
Give it a meaningful name and select the radio button: ‘Create Manually (Advanced)’:
![2-7](/assets/images/2-7.PNG)

### 3.
Tick ‘Performance Counter’ then click next:
![3-6](/assets/images/3-6.PNG)

### 4.
Click the ‘Add’ button:
![4-6](/assets/images/4-6.PNG)

### 5.
Expand the BranchCache Node, select BITS: Bytes from cache and BITS: Bytes from server then select the Add button.  Then Click OK:
![5-6](/assets/images/5-6.PNG)

### 6.
Click Next:
![6-5](/assets/images/6-5.PNG)

### 7.
Accept the default (or change it) save location, change credentials that it will *run as* if you need to then click finish.

### 8.
Right-click your newly defined Data Collector and select Start:
![7-5](/assets/images/7-5.PNG)

### 9.
Now at your branch office, install an application from SCCM on another computer ie the one that you are not monitoring with the data collector set.  This will then install from over the WAN and the content will be cached locally on the computers disk.  Once you’ve done that, on the computer that we are monitoring, install the same application.  This will install it from the content cached locally on the first computer.  We can see this by looking at the perfmon logs we just set up for monitoring:
![8-4](/assets/images/8-4.PNG)

### 10.
That’s it!   Don’t forget to turn off the perfmon collector set when you’ve finished.
