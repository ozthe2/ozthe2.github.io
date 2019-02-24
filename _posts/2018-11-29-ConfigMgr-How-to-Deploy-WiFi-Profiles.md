---
layout: post
title:  "ConfigMgr: How to Deploy WiFi Profiles Using PowerShell"
date:   2018-11-29 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr,powershell,deployment]
---
If you want to know how I deployed WiFi profiles to all users using ConfigMgr and PowerShell then you will want to read this post.

If, like me, you want to deploy WiFi profiles to your Windows 10 clients using ConfigMgr, you may decide to try the WiFi Profiles node found under Assets and Compliance in the ConfigMgr console as shown below:

![SCCM-WiFi-Prof1](/assets/images/SCCM-WiFi-Prof1.png)

And if, like me, you are not using certificates, but instead use passwords for WiFi access, you may think about exporting your existing WiFi profiles and importing the xml as shown below:

![SCCM-WiFi-Prof2](/assets/images/SCCM-WiFi-Prof2.png)

To view existing WiFi profiles:

`netsh wlan show profiles`

Then To Export a specific WiFi Profile to an xml file to import into ConfigMgr:

`netsh wlan export profile "type_profile_name_here" key=clear folder=c:\wifi`

Or to export all WiFi profiles into separate xml files:

 `netsh wlan export profile key=clear folder="c:\ohtemp\wifiprofiles"`

You can then deploy this profile to computers as you see fit - it ends up as a compliance item and it works perfectly.

Well...sort of.

When I tried it, it created the WiFi profile in the current logged on user context.  Whilst this may be OK for some, the issue was that there was no WiFi connection when the computer was sitting at the logon screen - only once a user had logged in, would it connect.

To rectify this, I wrote a PowerShell script and deployed the script using the Application method to my computers.  This deployed the WiFi profile to 'All Users' and thus would connect when sat at the login prompt. Excellent.

### How to use the script:
It's pretty simple to use and it creates a registry key that can be used as a detection rule in the ConfigMgr application.

You will need to place the script and the exported xml files (created by the netsh commands as mentioned above) in the same folder wherever you normally store your source files for ConfigMgr:

![Files](/assets/images/Files.png)

Then, create a new application, and choose 'Manual' etc etc then Script Installer for the deployment type.

For the 'Installation Program' use the following:

`powershell.exe -executionpolicy bypass -command "& {. .\New-OHWiFiProfile.ps1; new-ohwifiprofile -DeploymentVersion 1 }"`

![InstallPRog](/assets/images/InstallPRog.PNG)

And for the detection rule, simply detect the registry key and value that was used as the *DeploymentVersion* parameter:

![Detection-Rule](/assets/images/Detection-Rule.png)

If you add any profiles or change passwords simply update your xml files, change the parameter *DeploymentVersion* to a new unique number (I suggest going sequentially but whatever) and update the deployment.

In the registry you will get something like this:
![Registry](/assets/images/Registry.png)

Feel free to change names and locations by adjusting the PowerShell code.

Of course you could also make this a Compliance item instead of a deployed app should you wish to.

The script is fully documented and you can find it in my [Github repo here.](https://github.com/ozthe2/Powershell/blob/master/SCCM/New-OHWiFiProfile)
