#Install-ChocolateyZipPackage
`Install-ChocolateyZipPackage $packageName $url $unzipLocation`  
  
##Description
This will download a file from a url and unzip it on your machine. Has error handling built in. You do not need to surround this with try catch if it is the only thing in your [[chocolateyInstall.ps1|ChocolateyInstallPS1]].  

##Parameters
###$packageName
This is an arbitrary name.  
Example: `'7zip'`  
  
###$url (important)
The Url to the zip file.  
Example: `'https://github.com/downloads/spraints/git-tfs/GitTfs-0.11.0.zip'`  
  
###$unzipLocation (very important)
Where to unzip contents of the downloaded zip file.  
Example: `"$(Split-Path -parent $MyInvocation.MyCommand.Definition)"` - will install it to the tools folder of your package.  
  
###$url64bit (optional) - v0.9.8.14+
If there is a 64 bit installer available, put the link next to the other url. Chocolatey will automatically determine if the user is running a 64bit machine or not and adjust accordingly.  
Example: `'http://stexbar.googlecode.com/files/StExBar64-1.8.3.zip'`  
Defaults to the 32bit url.  
  
##Examples
`Install-ChocolateyZipPackage 'gittfs' 'https://github.com/downloads/spraints/git-tfs/GitTfs-0.11.0.zip' $gittfsPath`  
  
`Install-ChocolateyZipPackage 'sysinternals' 'http://download.sysinternals.com/Files/SysinternalsSuite.zip' "$(Split-Path -parent $MyInvocation.MyCommand.Definition)"`  
  
`Install-ChocolateyZipPackage 'sysinternals' 'http://download.sysinternals.com/Files/SysinternalsSuite.zip' "$(Split-Path -parent $MyInvocation.MyCommand.Definition)" 'http://download.sysinternals.com/Files/SysinternalsSuitex64.zip'`  
  
[[Helper Reference|HelpersReference]]