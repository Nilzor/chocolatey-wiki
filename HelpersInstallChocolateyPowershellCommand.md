#Install-ChocolateyPowershellCommand
`Install-ChocolateyPowershellCommand $packageName $psFileFullPath $url`  
  
##Description
This will install a powershell script as a command on your system. Like an executable can be run from a batch redirect, this will do the same, calling powershell with this command and passing your arguments to it. If you include a url, it will first download the powershell file. Has error handling built in. You do not need to surround this with try catch if it is the only thing in your [[chocolateyInstall.ps1|ChocolateyInstallPS1]].  

##Parameters
###$packageName
This is an arbitrary name.  
Example: `'installwindowsimage.powershell'`  
  
###$psFileFullPath (important)
The full path and name of the file to save or an existing file if $url is not included. This should include the name of the file and extension.  
Example: `Join-Path $(Split-Path -parent $MyInvocation.MyCommand.Definition) 'Install-WindowsImage.ps1'`  
  
###$url (optional)
The Url to the file.  
Example: `http://somewhere.com/downloads/Install-WindowsImage.ps1`  
   
###$url64bit (optional) - v0.9.8.14+
If there is a 64 bit installer available, put the link next to the other url. Chocolatey will automatically determine if the user is running a 64bit machine or not and adjust accordingly.  
Example: `'http://somewhere.com/downloads/Install-WindowsImagex64.ps1'`  
Defaults to the 32bit url.  
  
##Examples  
  
```powershell
$psFile = Join-Path $(Split-Path -parent $MyInvocation.MyCommand.Definition) "Install-WindowsImage.ps1"
Install-ChocolateyPowershellCommand 'installwindowsimage.powershell' $psFile 'http://somewhere.com/downloads/Install-WindowsImage.ps1'
```  
  
```powershell
$psFile = Join-Path $(Split-Path -parent $MyInvocation.MyCommand.Definition) "Install-WindowsImage.ps1"
Install-ChocolateyPowershellCommand 'installwindowsimage.powershell' $psFile 'http://somewhere.com/downloads/Install-WindowsImage.ps1' 'http://somewhere.com/downloads/Install-WindowsImagex64.ps1'
```  
  
```powershell
$psFile = Join-Path $(Split-Path -parent $MyInvocation.MyCommand.Definition) "Install-WindowsImage.ps1"
Install-ChocolateyPowershellCommand 'installwindowsimage.powershell' $psFile  
```  
  
[[Helper Reference|HelpersReference]]