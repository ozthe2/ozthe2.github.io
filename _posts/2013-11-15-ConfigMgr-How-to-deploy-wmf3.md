---
layout: post
title:  "ConfigMgr: How to Deploy Windows Management Framework 3.0"
date:   2013-11-15 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, wmf]
---

If you want to know how I deployed WMF 3.0 then you will want to read this post.

**Update**  To deploy WMF 4.0 see my post here.

By default, Windows 7 does not come with Powershell version 3.0 and that's reason enough to install WMF 3.0 on all of them.

You can download it from here: http://www.microsoft.com/en-gb/download/details.aspx?id=34595

Here's how I did it using Configuration manager 2012:

1.  Start by creating a new application and ensure that you select to : Manually specify the application information

![](/assets/images/wmf3/11.png)


2.  On the next screen, complete the fields as you see fit.  I also chose to allow this application to be installed from the task sequence as this is something I will probably add to my Windows 7 deployment task sequence soon.

![](/assets/images/wmf3/21.png)


3.  On the Application Catalog screen, fill in as much info as you desire.  Mine is minimalistic as I won't be making this application available in the catalog but will deploy the end result to a computer collection.

![](/assets/images/wmf3/32.png)

4.  For the Deployment Type, click the Add button.

![](/assets/images/wmf3/41.png)

5.  Ensure that you change the Type to 'Script Installer (Native)' and that you select 'Manually specify the deployment type information.'

![](/assets/images/wmf3/51.png)

6.  Enter some meaningful information to identify this particular deployment type:

![](/assets/images/wmf3/61.png)

7.  On the Content screen, browse to the location on your config manager server where you have placed the wmf.30 installer, then click the browse button for the installation program:

![](/assets/images/wmf3/7.png)

8.  Ensure that you select 'All Files' from the filter or you won't see the .msu file!

![](/assets/images/wmf3/81.png)

9.  Ensure that you complete the installation and uninstall fields as per the following screenshot.  I have chosen to suppress computer restarts so I added /quiet /norestart at the end of both command lines.  Please note the /uninstall switch added to the 'Uninstall Program' command line.  (It's really useful if you decide to uninstall WMF 3.0 for whatever reason!)

![](/assets/images/wmf3/9.png)


10.  Next up is the detection clause so click on the 'Add Clause' button.

![](/assets/images/wmf3/10.png)

11.  I chose to use the powershell.exe itself as the detection clause as in my tests I noticed that the .exe receives a version change on installation of WMF 3.0 making it a nice and easy method of detection for this installation.

For info, and if you wish to be extra precise, the vanilla powershell.exe on a fully patched Windows 7 has version 6.1.7600.13385 and after WMF 3.0 it has version 6.2.9200.16398.  But don't take my word for it, take a look yourself!

With that in mind, here's my detection rule:

![](/assets/images/wmf3/111.png)

12.  I will be installing this for the system and wish to deploy the finished app regardless of whether a user is logged on or not and I have therefore set my user experience settings to the following:

![](/assets/images/wmf3/12.png)

13.  We need to add some installation requirements so click the 'Add' button on the Requirements screen:

![](/assets/images/wmf3/13.png)

14.  The particular version of WMF 3.0 that I am deploying is specifically for Win 7 x64.  One of the WMF 3.0 requirements is that SP1 is installed so let's reflect this here:  (You may wish to season to taste and add disk space reqs or whatever meets your organisational needs etc.)

![](/assets/images/wmf3/14.png)

15.  Add any software dependencies that you want to ensure are installed first.  In my case I had none but your requirements may differ.

![](/assets/images/wmf3/15.png)

16.  Check the Summary screen and if you're happy and you know it click next:

![](/assets/images/wmf3/16.png)

17.  Hopefully, You have a success message:

![](/assets/images/wmf3/17.png)

18.  On the Deployment Types screen simply click the Next button:

![](/assets/images/wmf3/18.png)

19.  Check the Summary screen looks good then click Next:

![](/assets/images/wmf3/19.png)

20.  And you're done:

![](/assets/images/wmf3/20.png)

All you need to do now is to upload it to your distribution point and deploy it to either a computer collection or if you really feel the burning need to, make it available in the Application Catalog to your end users.