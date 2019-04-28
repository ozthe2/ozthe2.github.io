---
layout: post
title:  "ConfigMgr: How to Deploy .Net Framework"
date:   2013-11-28 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, powershell, deployment, dotnet]
---
If you want to know how I deployed .net framework using SCCM then you will want to read this post.

Deploying any version of .Net using Config Manager is straightforward once you have the detection rule for it.

This step-by-step guide will use .Net 4.5.1 as an example, deployed to Windows 7 computers.

If you wish to deploy the Windows Management Framework 4.0 to your Windows 7 SP1 computers then you will need to deploy .Net 4.5.1 as a pre-requisite first.

Here’s how I did it:

Firstly, you will need to download the offline installer for the framework and place the exe on your config manager server where you would normally place the files that you distribute.  I downloaded it from here: [http://www.microsoft.com/en-us/download/details.aspx?id=40779](http://www.microsoft.com/en-us/download/details.aspx?id=40779)

1.  Create a new Application

![net1](/assets/images/dotNet/net1.JPG) 

2.   Select “Manually specify the application information”

![net2](/assets/images/dotNet/net2.JPG) 

3.   Specify the application information.  I chose to Allow the application to be installed from the task sequence as I may do this at a later stage.

![net3](/assets/images/dotNet/net3.JPG)

4.  Fill in any details that you would like to appear in the Application Catalog.  I will not be making this available in the Application Catalog as I intend to deploy this to a computer collection so I left these fields at their defaults.

![net4](/assets/images/dotNet/net4.JPG) 

5.  Click the ‘Add’ button to create a new deployment type.

![net5](/assets/images/dotNet/net5.JPG) 

6.  Change the type to ‘Script Installer (Native)

![net6](/assets/images/dotNet/net6.JPG) 

7.   Give the Deployment type a meaningful name

![net7](/assets/images/dotNet/net7.JPG) 

8.  Browse to where you placed the installation .exe on your Config Manager server and complete the rest of the fields as shown in my screenshot below.  Note:  I chose to force a reboot suppression as I do not want computers having to restart at an inconvenient time to the end user.  Also note that I chose to “Run installation and uninstall program as 32-bit process on 64-bit clients” as I found that if I didn’t do this then the uninstallation of it would fail with a ‘16389’ error in the software centre.

![net8](/assets/images/dotNet/net8.JPG) 

9.  Click the ‘Add Clause’ button so that we can configure a detection rule for this deployment.

![net9](/assets/images/dotNet/net9.JPG) 

10. This next link holds the secret sauce that enables you to create a detection rule for any .net framework version: I looked here for the detection method:  [http://msdn.microsoft.com/en-us/library/ee942965(v=vs.110).aspx#detect_net](http://msdn.microsoft.com/en-us/library/ee942965(v=vs.110).aspx#detect_net)

With that in mind, ensure that your detection rule looks like mine (for a .net 4.5.1 deployment) in the screenshot below then click OK:

![netframework](/assets/images/dotNet/netframework.PNG)

11. Click Next

![net11](/assets/images/dotNet/net11.JPG)
 

12.  Set the Installation Behavior to : Install for system and the Logon Requirement to: Whether or not a user is logged on.

![net12](/assets/images/dotNet/net12.JPG) 

13.  Click the ‘Add’ button on the Requirements screen

![net13](/assets/images/dotNet/net13.JPG) 

14.  Add any system requirements that you would like for this deployment type.

![net14](/assets/images/dotNet/net14.JPG) 

15.  Click the next button at the Dependency screen unless you would like to add any.

![net15-1](/assets/images/dotNet/net15-1.JPG)

16.  Click Next at the deployment type summary

![net16-1](/assets/images/dotNet/net16-1.JPG)

17. If all has gone well you should have a successful message on the deployment type:

![net17-1](/assets/images/dotNet/net17-1.JPG)

18. Click Next on the Deployment Type screen

![net18-1](/assets/images/dotNet/net18-1.JPG)

19.  Click Next on the Summary

![net19-1](/assets/images/dotNet/net19-1.JPG) 

20.  If all went well you should have a success screen:

![net20-1](/assets/images/dotNet/net20-1.JPG)

21.  All that’s left is to upload the finished application to your distribution point and then deploy it to a computer collection.

---

**Get my book:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)