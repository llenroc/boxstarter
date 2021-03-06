# BoxStarter
Repeatable, reboot resilient windows environment installations made easy using Chocolatey packages
## For more information and How Tos, visit [the official Boxstarter website](http://boxstarter.org)

## Windows environment creation made easy!
* 100% Unattended Install with *pending reboot detection* and *automatic logon*.
* Remote machine deployments
* Integrates with Hyper-V and Windows Azure VMs supporting checkpoint restore and creation
* Installation packages build on top of [Chocolatey Nuget](http://chocolatey.org) package management
* Easily install with just a [Gist and the Boxstarter Web Launcher](http://boxstarter.org/WebLauncher) or [create a private repo on a Thumb drive or network share](http://boxstarter.org/InstallingPackages#InstallFromShare)
* Works on Window 7/2008 R2 and up with Powershell 2.0 and higher
* Lots of Windows configuration utilities including installing critical updates, changing windows explorer options, and more.

## Quickly Load up your favorite apps and settings on any machine with a gist! No preinstalled software needed
**Grab your Gist**
![gist](Web/Images/gist3.PNG)

**Launch the Boxstrter launcher**
![boxstarter weblauncher](Web/Images/start.png)

## Easily package installation scripts and resources in a Nuget package
**A simple Hello World**
```powershell
Import-Module Boxstarter.Chocolatey
New-BoxstarterPackage HelloWorld
Set-Content (Join-Path $Boxstarter.LocalRepo "HelloWorld\Tools\ChocolateyInstall.ps1") `
  -Value "Write-Host `"Hello World! from `$env:COMPUTERNAME`";CINST Git" -Force
Invoke-BoxstarterBuild HelloWorld
```

**Install on another machine**
```powershell
$creds=Get-Credential win7\mwrock
Install-BoxstarterPackage -ComputerName win7 `
  -Package HelloWorld -Credential $creds
```

![Remote Install](Web/Images/result.png)

NOTE: Powerhell Remoting must be enabled on the remote machine. Launch a Powershell Console as administrator:
```powershell
Enable-PSRemoting -Force
```
