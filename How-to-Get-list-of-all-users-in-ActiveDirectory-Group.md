Open PowerShell and type/copy one of the following commands

### Recursively Print all users and groups with ALL data
```ps
Get-AdGroupMember "it-appdevelopment" -Recursive
```
### Recursively Print all users only print globalId/name
```ps
Get-AdGroupMember "it-appdevelopment" -Recursive | 
  Select-Object SamAccountName
```
OR
```
Get-AdGroupMember "it-appdevelopment" -Recursive | 
  Select-Object name
```
### Recursively Print all users with GivenName, Surname, and globalId(name)
```ps
Get-AdGroupMember "it-appdevelopment" -Recursive | 
  Where-Object {$_.ObjectClass -eq 'User'} | 
  Get-ADUser -Properties Description | 
  Select-Object GivenName, Surname, name
```
### Recursively Print all users with GivenName, Surname, and globalId(name) but export to CSV to import into excel
```ps
Get-AdGroupMember "it-appdevelopment" -Recursive | 
  Where-Object {$_.ObjectClass -eq 'User'} | 
  Get-ADUser -Properties Description | 
  Select-Object GivenName, Surname, name | 
  Export-csv c:\reports\adGroupMembers.csv -NoTypeInformation
```

### Recursively Print all users to Text file
```ps
dsquery group -name "it-appdevelopment" | 
  dsget group -c -members -expand | 
  dsget user -c -samid -display > c:\reports\adGroupMembers.txt
```
### Other resources
Other PowerShell commands like this can be found in https://code.cmich.edu/explore/snippets

## Tags
[[ActiveDirectory]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ActiveDirectoryTag)
[[PowerShell]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PowerShellTag)