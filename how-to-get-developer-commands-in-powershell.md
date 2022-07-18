# Summary

This document provides instruction on setting Visual Studio Developer Command Prompt environment variables in PowerShell so that PowerShell and PowerShell ISE can be used for developing with the command line (such as for testing CI script commands).

# Background

The Visual Studio Developer Command Prompt is a standard Windows Command Prompt instance that sets environment variables specific to Visual Studio.  The environment variables give quick access to executables such as MSBuild, MSTest, devenv, etc.  The Developer Command Prompt shortcut simply runs a batch file when the Command Prompt opens.  However, PowerShell does not play nicely with batch files, so we can't simply run the same batch file to make PowerShell work as a developer command prompt.  Instead we can configure PowerShell and PowerShell ISE to parse the batch file and set the environment variables when they are launched.

# PowerShell Profile Scripts

When PowerShell and PowerShell ISE are launched, they will automatically attempt to load profile scripts, so this makes the profile script a good place to set the developer environment variables.  The default folder for profile scripts is in the `WindowsPowerShell` folder inside your `Documents` folder.  If you have re-mapped your home or documents folders to location other than `C:\Users\`, or if you want to verify the location for profile scripts, you can easily determine the profile script location:

  1.  Open PowerShell
  2.  Type `$profile`
  3.  Hit <kbd>ENTER</kbd>

PowerShell will display full path to the profile script it expects to find, even if the script doesn't exist.  Note that the path is the same for both PowerShell and PowerShell ISE, but that the script names are different.  By default, PowerShell uses `Microsoft.PowerShell_profile.ps1` and PowerShell ISE uses `Microsoft.PowerShellISE_profile.ps1` as profile scripts.

## Creating the Script Files

If your profile script files do not already exist, you will need to create them.  The easiest way to create the profile scripts is to launch PowerShell and run this command:

```powershell
New-Item ("Microsoft.PowerShell_profile.ps1", "Microsoft.PowerShellISE_profile.ps1" | %{ Join-Path (Split-Path -Path $profile) -ChildPath $_ }) -Type file -Force
```

This will create the appropriate script files for both PowerShell and PowerShell ISE.  However, if you have changed the registry to force PowerShell to use different script names, you will need to alter the command above with the appropriate names or create the script files manually.

*Note:  this command will also overwrite any existing scripts, so don't run it if you already have profile scripts!*  

## Setting the Environment Variables

The location of the batch file used to set the environment variables has changed from Visual Studio 2015 to Visual Studio 2017, so you will need to use slightly different commands, depending on which version you have installed.

For Visual Studio 2015, add the following commands to both PowerShell profile scripts:

```powershell
pushd 'C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools\'
cmd /c "VsDevCmd.bat & set" |
foreach {
	if($_-match"=") {
		$v = $_.split("=");
        set-item -force -path "ENV:\$($v[0])" -value "$($v[1])"
	}
}
popd

write-host "Visual Studio 2015 Command Prompt variables set." -ForegroundColor Yellow
```

For Visual Studio 2017, add these commands instead:

```powershell
pushd 'C:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\Common7\Tools'
cmd /c "VsDevCmd.bat & set" |
foreach {
	if($_-match"=") {
		$v = $_.split("=");
        set-item -force -path "ENV:\$($v[0])" -value "$($v[1])"
	}
}
popd

write-host 'Visual Studio 2017 Command Prompt variables set.' -ForegroundColor Yellow
```

These commands will read the batch file used by the Developer Command Prompt and set the appropriate environment variables.  If you already have commands in your profile scripts, you may add the new commands either before or after the existing code.

## Test the Configuration

Start PowerShell or PowerShell ISE.  You should see output similar to the following:

```
Windows PowerShell
Copyright (C) 2016 Microsoft Corporation. All rights reserved.

Visual Studio 2017 Command Prompt variables set.
Loading personal and system profiles took 692ms.
PS U:\>
```

## Execution Policy

When you start PowerShell or PowerShell ISE, you may get an error stating that your profile script cannot be loaded because running scripts is disabled.  If so, you will need to run the `Set-ExecutionPolicy` command.  Launch PowerShell as an administrator and then run the following command:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

By default, PowerShell's execution policy is `Restricted`, which means that scripts cannot be run (the execution policy may be `Undefined`, which is effectively `Restricted`).  

*Note:  `RemoteSigned` allows scripts to be run automatically without being signed by a trusted publisher.  However, downloaded scripts are blocked by default and must be unblocked before they can be run, so there are still some security measures in place even after changing the execution policy.  Do remember, though, that changing the execution policy will make your computer slightly less secure.*

For more information on execution policies, please consult the [Microsoft documentation](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/about_Execution_Policies?view=powershell-6).

## Tags
[[PowerShell]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PowerShellTag)
