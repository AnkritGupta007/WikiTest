# Error Description
When attempting to build or debug a project which accesses SAP, the error `LIBRFC32.DLL not found` occurs. This error occurs because the SAP GUI installer does not correctly install the librfc32 library.

# Fix
Two files need to be copied to your local machine.
1. Download [librfc32.dll.x64](https://centralmichigan.sharepoint.com/:u:/r/sites/EnterpriseSoftwareDevelopment931/Shared%20Documents/Application%20Development/libraries/SAP/librfc32.dll.x64?csf=1&web=1&e=87XuaD) to `C:\Windows\SysWow64` and remove the `.x64` extension.
2. Download [librfc32.dll.x86](https://centralmichigan.sharepoint.com/:u:/r/sites/EnterpriseSoftwareDevelopment931/Shared%20Documents/Application%20Development/libraries/SAP/librfc32.dll.x86?csf=1&web=1&e=F7rlKD) to `c:\windows\system32` and remove the `.x86` extension.

> NOTE: If this still does not work, try swapping `librfc32.dll` and placing the `.x64` version in `c:\windows\system32` and the `.x86` version in `c:\windows\SysWow64`.

## Tags
[[SAP]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SAPTag)