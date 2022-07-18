# Summary
When you get the Windows 10 1809 (April 2019) update or later, your previous install of **Active Directory Users and Computers**  through [Remote Server Administration Tools (RSAT) for Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=45520) will be missing or broken. You can **not** install it from  "Manage optional features" in Settings > "Add a feature". Below are the instruction that are proven to work.

## Steps to install RSAT for Admin Active Directory
1. Go to [Remote Server Administration Tools (RSAT) for Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=45520) and Click **Download**
1. Select ` [x] WindowsTH-RSAT_WS2016-x64.msu` and Download it to your machine
1. Run the installer for **WindowsTH-RSAT_WS2016-x64.msu** and follow the instructions
1. Reboot your machine
1. Click the **Start** menu in Windows and type "Active Directory"
1. You should now have **Active Directory Users and Computers** again


## Only references
- https://answers.microsoft.com/en-us/windows/forum/all/rsat-tools-missing-after-october-2018-windows-10/893e1b9e-3d2c-4c65-9679-b7d1ef7e2696

## Tags
[[ActiveDirectory]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ActiveDirectoryTag)