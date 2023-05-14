---
layout: post
title:  "Schedule PowerShell scripts with ease using New-OHScheduledTask function"
date:   2023-05-06 08:00:00 +0000
categories: powershell
tags: [powershell, taskscheduler]
---

Automating repetitive tasks is essential for many IT professionals and system administrators. One of the most useful tools for automating tasks on a Windows machine is PowerShell. However, scheduling PowerShell scripts to run at specific times can be a bit of a challenge. Fortunately, there is a solution: the `New-OHScheduledTask` function.

## What is New-OHScheduledTask?

The `New-OHScheduledTask` function is a PowerShell cmdlet that creates a new scheduled task. It is a powerful tool that can help you automate a wide range of tasks, from running PowerShell scripts to launching applications and running batch files.


## How to Use New-OHScheduledTask

To create a new scheduled task using the `New-OHScheduledTask` function, you first need to specify the task's properties, such as the task name, the program or script to run, and the schedule for running the task. The  function has been optimmised to quickly schedule PowerShell scripts although it can just as easily schedule an exe. As I use it in my workplace primarily for Powershell, I'll focus the examples on that:

### Example 1: Deploying a simple PowerShell script

```powershell
New-OHScheduledTask -TaskName "MyTask" -TaskDescription "Runs a simple PowerShell script." -Trigger AtStartup -AllowedUser 'NT AUTHORITY\SYSTEM' -ScriptPath "c:\ohtemp\test2.ps1" -Action replace -RunWithHighestPrivilege

```
This example creates a new scheduled task named "MyTask" that runs a simple PowerShell script at system startup. The task is set to replace any existing task with the same name, and it will run with the highest privileges.

### Example 2: Deploying a complex PowerShell script
```powershell
New-OHScheduledTask -TaskName "MyTask" -TaskDescription "Runs a PowerShell script with lots of arguments." -Trigger AtStartup -AllowedUser 'NT AUTHORITY\SYSTEM' -Program "C:\Windows\System32\WindowsPowerShell\v1.0\PowerShell.exe" -Arguments '-noprofile -executionpolicy bypass -command "& { . c:\ohtemp\test2.ps1; Show-Text -textToDisplay "Important Text!" }' -Action add -RunWithHighestPrivilege
```
This example creates a new scheduled task named "MyTask" that runs a PowerShell script with lots of arguments, at system startup. The task is set to add a new task as long as the task name does not already exist, and it will run with the highest privileges. The PowerShell script in this example displays the text "Important Text!" using the Show-Text function contained in the script.

### Example 3: Deleting a Scheduled Task
```powershell
New-OHScheduledTask -TaskName "MyTask" -Delete
```
This example deletes the task named, "MyTask" if it exists.

## Conclusion

In conclusion, the `New-OHScheduledTask` function is a powerful tool that can help you automate a wide range of tasks on your Windows machine. Whether you need to run a PowerShell script, launch an application, or execute a batch file, this function can help you get the job done. The function's customizable parameters allows you to create scheduled tasks quickly and efficiently and you can find it in my GitHub repo: https://github.com/ozthe2/MyPowerShell/blob/main/New-OHScheduledTask.


---


"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)