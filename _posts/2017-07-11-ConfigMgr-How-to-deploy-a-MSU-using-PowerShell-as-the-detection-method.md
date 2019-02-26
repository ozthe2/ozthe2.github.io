---
layout: post
title:  "ConfigMgr: How to deploy a MSU using PowerShell as the detection method"
date:   2017-07-11 22:00:00 +0000
categories: ConfigMgr
tags: [configmgr,powershell,deployment]
---
I have documented my approach on using PowerShell as a detection clause when deploying MSU files as it's something that I have done many times but never blogged the process.

Here is the table I used as a reference that I stole from Technet that explained what I needed to do in the PowerShell code in order to signify a successful installation…simply write to the host!  (stdout)
![1](/assets/images/DeployMSU/1.PNG)

Table referenced here:  https://technet.microsoft.com/en-gb/library/gg682159.aspx

So with that brief introduction out of the way, let's do this step-by-step:

Start by creating a new application in the SCCM console:
![2](/assets/images/DeployMSU/2.PNG)

![3](/assets/images/DeployMSU/3.PNG)

![4](/assets/images/DeployMSU/4.PNG)

![5](/assets/images/DeployMSU/5.PNG)

![6](/assets/images/DeployMSU/6.PNG)
For the installation program I use the following:
`wusa.exe "File.msu" /quiet /norestart`

And for the Uninstall program, (my screenshot below for the uninstall is slightly incorrect) I use this:
`wusa.exe /uninstall "File.msu" /quiet /norestart`

![7](/assets/images/DeployMSU/7.PNG)

![8](/assets/images/DeployMSU/8.PNG)

And here’s where the magic happens…(You can ‘Write-Host’ anything you like here, I used “Installed!” but as long as you write something to the stdout stream it will signify a successful detection.)

I’m not going to explain the PowerShell as it’s pretty obvious what’s going on…and yes…I know I can shorten all of this to one line but it’s more flexible and readable this way, so there!

*You will obviously need to replace 'KB40222720', as in my example below, with the hotfix ID of the msu that you are deploying.  To be sure of obtaining the correct  HotfixID simply install the msu on a computer manually, and then in PowerShell run `Get-Hotfix` which will list all of the installed hotfixes and their relevant HotfixID numbers:*
![Capture](/assets/images/DeployMSU/Capture.PNG)

Here's the code to save you typing:
`$UpdatesInstalled = Get-Hotfix 'KB40222720' -ErrorAction SilentlyContinue`
`If ($UpdatesInstalled) {`
    `Write-Host "Installed"`
`}`

![9](/assets/images/DeployMSU/9.PNG)

![10](/assets/images/DeployMSU/10.PNG)

![11](/assets/images/DeployMSU/11.PNG)

Your requirements may differ from mine..
![12](/assets/images/DeployMSU/12.PNG)

![13](/assets/images/DeployMSU/13.PNG)

![14](/assets/images/DeployMSU/14.PNG)

![15](/assets/images/DeployMSU/15.PNG)

![16](/assets/images/DeployMSU/16.PNG)

![17](/assets/images/DeployMSU/17.PNG)

![18](/assets/images/DeployMSU/18.PNG)

![19](/assets/images/DeployMSU/19.PNG)

That's all there is to it.
Leave a comment below if this helped you out!