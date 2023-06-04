---
layout: post
title:  "How to Automate Registry-Related Tasks with Set-OHRegistry PowerShell Function"
date:   2023-04-30 09:00:00 +0000
categories: PowerShell
tags: [powershell,registry]
---

At work, I needed to write a PowerShell function that would modify the Windows registry by creating, replacing, or deleting a specified registry key value. After some development and testing, I created a function called "Set-OHRegistry," which takes five parameters to complete the required task.

The five parameters of the Set-OHRegistry PowerShell function are:

- 'Path': the path to the registry key (e.g., HKCU:\Software\Microsoft).
- 'Name': the name of the registry key value (e.g., '(Default)' or 'UninstallString').
- 'Type': the data type of the registry key value (e.g., 'DWORD' or 'STRING').
- 'Value': the value associated with the name (e.g., 0 or 'C:\program files\myProgram\uninstall.exe').
- 'Action': the action to be performed on the registry: 'Create', 'Replace', or 'Delete'.

![](/assets/images/modifyreg.png)

## Parameters

Let's go through each of the parameters in more detail.

To modify the registry, you first need to specify the registry key you want to modify. This is where the 'Path' parameter comes in. The 'Path' parameter takes a string that specifies the registry key path. For example, you might specify HKCU:\Software\Microsoft.

The 'Name' parameter specifies the name of the registry key value you want to modify. For example, you might specify 'UninstallString'.

The 'Type' parameter specifies the data type of the registry key value. This can be 'DWORD', 'STRING', 'BINARY', or other data types supported by the Windows registry.

The 'Value' parameter specifies the value you want to associate with the name. For example, you might specify 'C:\program files\myProgram\uninstall.exe' or 0.

Finally, the 'Action' parameter specifies the action you want to perform on the registry. This can be 'Create', 'Replace', or 'Delete'.

```
Set-OHRegistry -path 'HKCU:\SOFTWARE\OHTesting' -name "Entry1" -type String -value "Some Data" -Action Replace
```
## Breakdown of Actions

To perform the appropriate action based on the user input, I utilized a switch statement. If the action is "Create" and the path does not exist, the function will create the path, name, type, and value. If the path exists but there is no data/value, it will create the name with the value. If the path, name, and value already exist, the function will exit.

If the action is "Replace," the function acts similarly to 'Create', except that if the path, name, and value already exist, it will replace type and value with the new type and value.

If the action is "Delete," the function will delete the registry data (Name) and value pair. It leaves the path intact.

## Function Improvements

One way you may wish to improve the function is to use Write-Verbose instead of Write-Host, as Write-Verbose allows users to selectively view detailed information during script execution. When you use Write-Verbose, the output will only appear in the console if the user explicitly specifies the -Verbose switch when running the script. This is especially useful for long-running scripts or scripts that perform complex tasks.

However, for my work task, I required Write-Host. Additionally, the function could be further improved by using a ValidateSet for the action type. For my requirements though, I needed to ensure that a terminating error was not produced if an incorrect action type was entered so chose to add it as the default option in the switch.  I've left the 'validateset' in the parameter but commented it out in case you prefer it.  Just uncomment it and then remove the whole 'default' line in the switch.

And if my "mega-all-in-one-function" is all a bit too much, you can use the PowerShell best practice versions [here](https://fearthepanda.com/powershell/2023/06/04/automate-registry-with-powershell_pt2/) instead.

## Conclusion

Overall, the Set-OHRegistry PowerShell function is a useful tool for modifying the Windows registry. While it could be improved in certain ways, it is a solid solution for those looking to automate registry-related tasks. The script is available on my GitHub repository: https://github.com/ozthe2/MyPowerShell/blob/main/Modify-OHRegistry.ps1

---


"Understanding Microsoft Intune: Deploying Applications Using PowerShell" is available for purchase at all good book stores and online outlets. Don't miss out on the opportunity to take your application deployment skills to the next level. Get your copy today!

[Amazon.co.uk](https://www.amazon.co.uk/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=asc_df_1484288491/?tag=googshopuk-21&linkCode=df0&hvadid=606535180727&hvpos=&hvnetw=g&hvrand=12156935864725452536&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9045778&hvtargid=pla-1897625803371&psc=1&th=1&psc=1)

[Amazon.com](https://www.amazon.com/Understanding-Microsoft-Intune-Applications-PowerShell/dp/1484288491/ref=sr_1_1?crid=2K98Q1E7TIKLJ&keywords=understanding+intune&qid=1682103272&sprefix=understanding+intune%2Caps%2C157&sr=8-1)

[Apress](https://link.springer.com/book/10.1007/978-1-4842-8850-4?source=shoppingads&locale=en-gb&gclid=CjwKCAjw6IiiBhAOEiwALNqncSKm2i93L3ZU_g23RICE6TxylXFk6HPq6YS6HLgsqr_vtCFbzQJMORoCFXUQAvD_BwE)


![](/assets/images/Apress_Intune.png)