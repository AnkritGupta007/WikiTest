## Summary
Easily get correlation id with powershell

``` shell
$ver = $host | select version
if ($ver.Version.Major -gt 1) {$host.Runspace.ThreadOptions = "ReuseThread"}
if ((Get-PSSnapin "Microsoft.SharePoint.PowerShell" -ErrorAction SilentlyContinue) -eq $null) {
    Add-PSSnapin "Microsoft.SharePoint.PowerShell"
}
 
 
#$serverlist = @("sp-prdweb02","sp-prdweb01","sp-prdweb03","sp-prdweb04")
$serverlist = @("SP-STGWEB01","sp-stgweb02")
#$serverlist = @("SP-prdweb04")
#$serverlist = @("it-devspweb01")
#$serverlist = @("IT-RES13WEB2")
#$serverlist = @("it-129287-2012s")
 
 
$logLocation = "\D$\0-SPData\ULSLogs"
#$logLocation = "\C$\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\LOGS\"
 
$corr = "*feac469d-2b6d-6075-eef5-e3464595ee85*"
$eventarray = @()
foreach ($server in $serverlist){
    $dir = '\\' + $server + $logLocation
    $dir
    $server
    Get-SPLogEvent -Directory $dir -StartTime '11/30/2015 8:40 AM'  -EndTime '11/30/2015 8:50 AM'   | ?{ $_.correlation -eq $corr } | Out-GridView
}
 
Out-GridView
```

## Tags
[[PowerShell]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PowerShellTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)