---
layout: post
title:  "Function New-OHShortcut: Create and Manage Shortcuts with PowerShell"
date:   2023-05-14 08:00:00 +0000
categories: powershell
tags: [powershell, shortcuts]
---


If you're a Windows user, chances are you use shortcuts to quickly access your favorite programs and files. Shortcuts are an essential part of the user experience, and they can help you save time and improve your productivity. However, creating and managing shortcuts can be a time-consuming and tedious task. That's where the New-OHShortcut function comes in handy. I wrote this for work last week and this PowerShell function allows you to create and manage shortcuts with ease.

## What is New-OHShortcut?

New-OHShortcut is a PowerShell function that creates or deletes a shortcut to a specified item on the desktop and/or start menu. It uses Windows Script Host to create the shortcut file, which is a convenient and reliable way to create shortcuts on Windows.

The function is designed to seamlessly integrate with various deployment software, such as Intune or ConfigMgr, utilising the system account. By default, it creates shortcuts on the public desktop and all users start menu. However, if you prefer to place the shortcut on the desktop of the currently logged-in user, simply include the "-UseLoggedInUsersDesktop" switch when invoking the function. Similarly, if you wish to add the shortcut to the logged-in user's start menu, use the "-UseLoggedInUsersStartMenu" switch.

## How to Use New-OHShortcut

Using New-OHShortcut is easy. Here's a quick guide to get you started:

### Creating a Shortcut

To create a shortcut, you need to specify the following parameters:

- **ShortcutName**: The name of the shortcut.
- **TargetPath**: The path of the item that the shortcut opens.
- **IconLocation**: The location of the icon for the shortcut.
- **AddLocation**: The location of the shortcut to add: Desktop, StartMenu, or Both.

Here's an example:
```
New-OHShortcut -ShortcutName "Notepad" -TargetPath "C:\Windows\System32\notepad.exe" -AddLocation Desktop -IconLocation "C:\Windows\System32\notepad.exe"
```

This command creates a shortcut to Notepad on the desktop.

### Replacing a Shortcut

To replace an existing shortcut, you need to specify the following parameters:

- **ShortcutName**: The name of the shortcut.
- **TargetPath**: The path of the item that the shortcut opens.
- **IconLocation**: The location of the icon for the shortcut.
- **ReplaceLocation**: The location of the shortcut to replace: Desktop, StartMenu, or Both.

Here's an example:
```
New-OHShortcut -ShortcutName "MyApp" -ReplaceLocation Both -TargetPath "C:\Program Files\MyApp\MyApp.exe" -IconLocation "C:\Program Files\MyApp\MyApp.exe"
```
This command replaces the shortcut to MyApp on the desktop and in the Start menu.

### Deleting a Shortcut

To delete a shortcut, you need to specify the following parameters:

- **ShortcutName**: The name of the shortcut.
- **DeleteLocation**: The location of the shortcut to delete: Desktop, StartMenu, or Both.

Here's an example:
```
New-OHShortcut -ShortcutName "MyApp" -DeleteLocation Both
```
This command deletes the shortcut to MyApp on the desktop and in the Start menu.

## Parameter Breakdown

Let's dive into a detailed breakdown of the function's full set of parameters. 

- **ShortcutName**: Specifies the name of the shortcut.
- **TargetPath**: Specifies the path of the item that the shortcut opens.
- **WorkingDirectory**: Specifies the working directory for the target. (Optional)
- **IconLocation**: Specifies the location of the icon for the shortcut. (Optional)
- **WindowsStyle**: Specifies the window style for the shortcut. Valid values are 3, 7, and 4. (Default: 7)
- **AddLocation**: Specifies the location where the shortcut will be added. Valid options are Desktop, StartMenu, or Both.
- **ReplaceLocation**: Specifies the location of the shortcut to replace. Valid options are Desktop, StartMenu, or Both.
- **DeleteLocation**: Specifies the location of the shortcut to delete. Valid options are Desktop, StartMenu, or Both.
- **Arguments**: Specifies the arguments to use when opening the target. (Optional)
- **UseLoggedInUsersDesktop**: Includes this switch if you want to position the shortcut on the desktop of the currently logged-in user.
- **UseLoggedInUsersStartMenu**: Includes this switch if you want to add the shortcut to the logged-in user's start menu.

Please note that for the parameters *WorkingDirectory*, *IconLocation*, *Arguments*, and the switches *UseLoggedInUsersDesktop* and *UseLoggedInUsersStartMenu*, they are optional and have default behavior unless specified.

## Final Thoughts

*New-OHShortcut* is a powerful PowerShell function that simplifies the process of creating and managing shortcuts on Windows. Whether you need to create a new shortcut, replace an existing one, or delete a shortcut, New-OHShortcut has got you covered. Give it a try, and see how it can improve your productivity! Find it in my github repo here: https://github.com/ozthe2/MyPowerShell/blob/main/New-OHShortcut.ps1

---


"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)