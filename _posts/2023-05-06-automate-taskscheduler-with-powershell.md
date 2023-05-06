---
layout: post
title:  "Schedule PowerShell scripts with ease using New-OHScheduledTask function"
date:   2023-05-06 08:00:00 +0000
categories: powershell
tags: [powershell, taskscheduler]
---

As a PowerShell user, scheduling PowerShell scripts is something you might have done frequently. However, it can be a time-consuming process that requires a lot of repetitive work. At my workplace we schedule a lot of PowerShell scripts and fortunately, with the New-OHScheduledTask function, scheduling PowerShell scripts has never been easier. 

The New-OHScheduledTask function is a PowerShell function that creates a new scheduled task in the Task Scheduler to run a specified PowerShell script. This function is designed to provide users with an easy method to schedule PowerShell scripts and allows them to specify task details such as the name of the scheduled task, the trigger, allowed user, script path, delay time, task folder, and much more. 

The function begins by checking if the specified script path exists before proceeding with the creation of the scheduled task. If the script path does not exist, the user will be notified, and the function will return. Next, the function checks if the user specified a task name; if no name was specified, it uses the leaf name of the script path instead.

New-OHScheduledTask has several optional parameters that can be used to customize the scheduled task to meet your needs. For example, the -Trigger parameter allows you to specify when the task should run. The options available are "AtLogon" and "AtStartup." If you want to specify a delay time before the scheduled task runs, the -DelayTask parameter can be used. The options available are "1s", "1m", "30m", and "1h."

The -TaskFolder parameter allows you to specify the folder to store the scheduled task in. If you don't specify a folder, the function will create a folder named "OHTesting" so be aware of this as you may wish to change it. The -AllowedUser parameter allows you to specify the user account that is allowed to run the scheduled task. The options available are "BUILTIN\Users" and "NT AUTHORITY\SYSTEM." 

Additionally, the function has three switch parameters: *-RunWithHighestPrivilege*, *-StartTaskImmediately*, and *-DeleteExistingTask*. The -RunWithHighestPrivilege parameter indicates that the scheduled task should run with the highest privilege. The -StartTaskImmediately parameter indicates that the scheduled task should be started immediately after creation. The -DeleteExistingTask parameter indicates that an existing task with the same name should be deleted before creating a new one.

To demonstrate how to use the New-OHScheduledTask function, consider the following examples:

## Example 1:
```
New-OHScheduledTask -TaskName "MyTask" -ScriptPath "C:\Scripts\MyScript.ps1" -AllowedUser "NT AUTHORITY\SYSTEM" -Trigger "AtStartup" -RunWithHighestPrivilege -StartTaskImmediately
```

This example creates a scheduled task named "MyTask" to run "C:\Scripts\MyScript.ps1" at startup, allows "NT AUTHORITY\SYSTEM" to run the task, runs the task with the highest privilege, and starts the task immediately after creation.

## Example 2:
```
New-OHScheduledTask -ScriptPath "C:\Scripts\MyScript.ps1" -AllowedUser "BUILTIN\Users" -DelayTask "30m"
```

This example creates a scheduled task to run "C:\Scripts\MyScript.ps1" with a 30-minute delay and allows "BUILTIN\Users" to run the task.

In conclusion, the New-OHScheduledTask function is a handy tool that simplifies the process of scheduling PowerShell scripts. The function's customizable parameters allows users to create scheduled tasks quickly and efficiently and you can find it in my GitHub repo: https://github.com/ozthe2/MyPowerShell/blob/main/New-OHScheduledTask.


---


"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)