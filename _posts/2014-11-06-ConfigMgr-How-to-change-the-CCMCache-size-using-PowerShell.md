---
layout: post
title:  "ConfigMgr: How to Change the CCMCache Size Using PowerShell"
date:   2014-11-06 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr, powershell, posh, ccmcache]
---

If you would like to deploy a CCMCache size change to computers using ConfigMgr and PowerShell then you will want to read this step-by-step guide..…



## 2019 Update
Ooohhh.... did I really do it this way?  

1. How do we know that the cache size has *actually* taken place?
2. We don't need to write to the registry do we?  I mean,  DO WE! No..you're right - we don't.

OK, yeah, I mean the method described below will work and get you out of a bind but there's just *gotta* be a better way right? RIGHT?

[Yeah, there is.](https://leanpub.com/configmgr-DeployUsingPS)

For those of you that still want to use my original, "get you out of a bind" method, then read on!


I recently needed to change the CCMCache size on a few hundred computers and this was my approach to doing it via an SCCM application deployment using a PowerShell script to make the cache size change.

This post may seem daunting, but I can assure you that you do not need to understand PowerShell if you follow this guide.  Take the time to read it slowly in the order presented and you will have it licked in no time.

As usual, let's do this step-by-step:

### 1 - Pre-req's:
The first thing I did was write a Powershell script to do the task in hand.  When calling the script from the command line, you can use the parameter -CacheSize followed by the number in MB that you want to size it to.  If you leave this parameter out then it defaults to setting it to 10GB.  By including this parameter in the script we now give ourselves the ability of using one application with multiple deployment types – awesome!   The script will also write to the local computers registry which I use not only for the detection rule but also it’s nice to be able to pull this information into a report if needed at a later stage.

Having said all of that, you can [find the script here in my Github repo](https://github.com/ozthe2/Powershell/blob/master/SCCM/SetCCMCacheSize), it’s called: SetCCMCacheSize.ps1

If you wish to change the *default* setting of 10GB  – then you will need to adjust the figure (in MB) on line 4 that reads:

`$CacheSize = 10240`

*Remember, this is just the default cache size setting - we will be changing this **dynamically** in our SCCM application that we are about to create.  This will become clearer as you continue to read through this post.*

And finally, you may wish to adjust where it writes the information into the registry by editing line: 49:

```powershell
New-Item -Path HKLM:\System\CSU\CCMCache -force
```

and line 52:

```powershell
New-ItemProperty -path HKLM:\System\CSU\CCMCache -name 'SizeInMB' -Value $Size -PropertyType string -force
```

Once that’s done, simply save the .ps1 file to where ever you would normally store your apps\scripts source files that you distribute, on your Configuration Manager server.

### 2 – Now to create the Application:

**a:** In the Configuration Manager Console, select Create Application as you would normally:

![1-2](/assets/images/1-2.PNG)

**b:** Select ‘Manually specify the information’:

![2-2](/assets/images/2-2.PNG)

**c:** Complete the fields you are interested in on the General Information screen:

![3-2](/assets/images/3-2.PNG)

**d:** I never completed anything for the Application Catalog as I will be deploying this to devices, however, feel free to season to taste:

![4-2](/assets/images/4-2.PNG)

**e:** Click the ‘Add’ button to add a new deployment type:

![5-2](/assets/images/5-2.PNG)

**f:** Select ‘Script Installer’ and ‘Manually specify the deployment type information’:

![6-1](/assets/images/6-1.PNG)

**g:** Give the deployment type a meaningful name.  *In my example, I will be setting the cache size to 6GB:

![7-1](/assets/images/7-1.PNG)

**h:** In the content Location field, Browse to the folder where you stored your powershell script and for the installation program type:

```powershell
powershell -ExecutionPolicy Bypass -file .\SetCCMCacheSize.ps1 -cachesize 6144
```

If you want it set to 10GB then you can leave off the parameter -cachesize 6144 entirely.  Likewise if you wanted it set the cache size to a different figure, say 8GB then you would use the following:

```powershell
powershell -ExecutionPolicy Bypass -file .\SetCCMCacheSize.ps1 -cachesize 8192
```

1024 = 1GB so you need to use multiples of this number for the CacheSize parameter value.

Example, if you wanted a 2 GB cache size, then the number you would use is 2048
(1024 x 2 = 2048)

![8-1](/assets/images/8-1.PNG)

**i:** Click the ‘Add Clause’ button:

![9-1](/assets/images/9-1.PNG)

**j:** For the detection rule, complete the settings as shown in my screenshot below, however, if you have changed the script to write to a different part of the registry then you will need to reflect that change here.  Also, make sure that the ‘Value’ is set to the same figure that you use as the parameter in step h (above) eg it must match the size that you are setting the cache to.  Continuing my example, I am setting it to 6GB so the value is: 6144

![10-1](/assets/images/10-1.PNG)

**k:** Here’s the result of your detection rule:

![11-1](/assets/images/11-1.PNG)

**l:** For the user experience, I will be deploying to devices and so I have completed the fields as shown below in my screenshot:

![12-1](/assets/images/12-1.PNG)

**m:** Click the ‘Add’ button to add some system requirements for this deployment type.

![13-1](/assets/images/13-1.PNG)

**n:**  I just chose Windows 7 SP1 x64 but your needs may differ:

![14-1](/assets/images/14-1.PNG)

**o:** The result of your requirements:

![15-1](/assets/images/15-1.PNG)

**p:** If you want to add any dependencies then do it here.  I chose not to:

![16-1](/assets/images/16-1.PNG)

**q:** Close the summary screen:

![17-1](/assets/images/17-1.PNG)

**r:**  The Deployment Type Wizard summary:

![18-1](/assets/images/18-1.PNG)

**s:** Here’s where you can add another deployment type.  You could click the 'Add' button if you wanted to and repeat the above process and have multiple different cache sizes depending on the requirements.  Cool stuff! I simply clicked ‘Next’ here for this example though:

![19-1](/assets/images/19-1.PNG)

**t:** You are presented with a Summary:

![20](/assets/images/20.PNG)

**u:** And you’re done!

![21](/assets/images/21.PNG)

### 3.  Here’s what it looks like in Config Manager:

![22](/assets/images/22.PNG)

Now you simply need to upload this to your distribution point and deploy to a computer collection.  I made mine a required deployment.

### 4.  Here’s what you get in the registry on the computer that has successfully had its cache size changed:

![23](/assets/images/23.PNG)

### 5. And the resulting cache size on the computer:

![24](/assets/images/24.PNG)

---

**Get my book:**

[ConfigMgr - An Administrator's Guide to Deploying Applications using PowerShell](https://leanpub.com/configmgr-DeployUsingPS)