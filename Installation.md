# Installing Chocolatey
There are a few ways to install chocolatey. Chocolatey exists as a [nuget package](http://nuget.org/list/packages/chocolatey) so virtually any way you can get a nuget package, you have the opportunity to then install it.  

If you have Visual Studio 2010 and the NuGet extension installed, perhaps the quickest method is to use NuGet Package Manager. Three commands in succession and you are done. See it below.  

## PowerShell
This is the easiest method. Open a powershell command line and run the following:  
  
```powershell
# variables
$url = "http://packages.nuget.org/v1/Package/Download/Chocolatey/0.9.8.4"
$chocTempDir = Join-Path $env:TEMP "chocolatey"
$tempDir = Join-Path $chocTempDir "chocInstall"
if (![System.IO.Directory]::Exists($tempDir)) {[System.IO.Directory]::CreateDirectory($tempDir)}
$file = Join-Path $tempDir "chocolatey.zip"

# download the package
Write-Host "Downloading $url to $file"
$downloader = new-object System.Net.WebClient
$downloader.DownloadFile($url, $file)

# unzip the package
Write-Host "Extracting $file to $destination..."
$shellApplication = new-object -com shell.application 
$zipPackage = $shellApplication.NameSpace($file) 
$destinationFolder = $shellApplication.NameSpace($tempDir) 
$destinationFolder.CopyHere($zipPackage.Items(),0x10)

# call chocolatey install
Write-Host "Installing chocolatey on this machine"
$toolsFolder = Join-Path $tempDir "tools"
$chocInstallPS1 = Join-Path $toolsFolder "chocolateyInstall.ps1"

& $chocInstallPS1

# update chocolatey to the latest version
Write-Host "Updating chocolatey to the latest version"
cup chocolatey
```
  
## PowerShell Through Batch Method
This is the best method if you want to repeat it or include it in source control. It requires no change to your existing powershell to allow for remote unsigned scripts.  

Download the two items from [chocolateyInstall](https://github.com/ferventcoder/chocolatey/tree/master/chocolateyInstall).  
  
Run `installChocolatey.cmd` and it will install and update to the latest version of chocolatey.  
  
## NuGet Package Manager Method
  
When you have Visual Studio 2010 and the NuGet extension installed, you can simply type the following three commands and you will have chocolatey installed on your machine.  
  
 `Install-Package chocolatey`  
 `Initialize-Chocolatey`  
 `Uninstall-Package chocolatey`  

## NuGet.exe + PowerShell Method

You can also use nuget command line to download chocolatey:  
  
 `nuget install chocolatey`  
  
Once you download it, open powershell (remote unsigned) and run:  

 `Initialize-Chocolatey`