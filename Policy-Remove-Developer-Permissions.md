# Remove Developer Permissions
This page documents all information and removal required for when a developer leaves the team, with links to more specific documentation where appropriate.

## Exit Checklist

### Remove Global ID from ActiveDirectory Groups We Control
  * Remove to AD Group depending on type of hire: (all group is within `IT-AppDevelopment`)
      * **Contractors:** Remove from `IT-AppDevelopment-Contractor` and `IT-AppDevelopment-Contractor-Admin`
      * **Students:** Remove from `IT-AppDevelopment-Student` and `IT-AppDevelopment-Student-Admin`
      * **Direct Hires:** Remove from `IT-AppDevelopment-Staff` and `IT-AppDevelopment-Staff-Admin`
  * Remove from Microsoft Teams: [AppDevelopment](https://teams.microsoft.com/_#/teamDashboard//19:02d7168b651e4b3f90a1b7404d13201a@thread.skype/td.members) , Other project teams, etc.
  * Remove access to https://centralmichigan.sharepoint.com/sites/ApplicationDevelopmentTeam (Member Access)
  * Remove access to https://centralmichigan.sharepoint.com/sites/EnterpriseSoftwareDevelopment931 (Member Access)
    * Remove from Outlook groups 
      * https://outlook.office365.com/people/group/groups.cmich.edu/applicationdevelopmentteam
      * https://outlook.office.com/people/group/groups.cmich.edu/softwareengineeringdevelopmentteam
  * Removed Gitlab Permissions
      * https://code.cmich.edu/groups/IT-AppDevelopment/-/group_members and run the `Sync now`
      * Double check that they have been removed from Membership as they are removed from the AD Groups
  * Remove from Dev Team/Dev Student Outlook Group `appdevelopment@groups.cmich.edu`
  * Remove from Bi-Weekly Team Meeting
  * Remove them from `IT-AppDevelopment-VisualStudio` (signing into AD with your IT- account) to reclaim a Visual Studio group license

### Remove them from our Resharper group license with [CMU Web Applications Support](https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=14955)
   - Title: Remove Developer from from our Resharper group license 
   - Description: "We have a Software Developer who has left their position. Please have a Team Lead remove globalId '_____' from our Resharper group license at https://account.jetbrains.com/organization/357761"
   - CMU Web Application: **Other/Not Listed**

### Remove TDx Permission with [TeamDynamix Access Request](https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=22333)
  - Title: "TeamDynamix Access Request" (uneditable on the form)
  - Description: "We have a Software Developer who has left their position and we need to have their Tdx project and ticket permissions removed, or confirmed if removed already. Their globalId is '_______'."

### Remove from VDI with [Developer Virtual Desktop Request](https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=22357)
  - Title: Remove developer from it-vdi-developers-users and removed from virtual machine
  - Description: "We have a software developer who has left their position and we need to have their globalID removed from VM 'it-vdi-dev__'. We already let them know to grab an active work or files, so it can be re-imaged if it is not a shared resource with others. Their globalId is '_______'.

### Delete it-{globalId} account and remove globalId from it-vdi-developers-users with [Active Directory Management](https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=15012)
> ℹ **Note**: Only **After** you have confirmed the developers VM machine name in VMWare, i.e., 'it-vdi-dev__', should you put in **this** request.
  - Title: Remove and confirm AD Group removal for a developer 
  - Description: "We have a software developer who has left their position and we need to have their it-globalId account removed and to have their globalId removed from AD group it-vdi-developers-users. Their globalId is '_______'." 
  - **If they are a student develop** mention in the Description "They are a student developer and need to be removed from `\\IT-STORM\IT-StuEmp$\StudentEmployees.txt`."

### Remove VPN Permission with [Wired and Wireless Network Support](https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=22329)
  - Title: Remove and confirm VPN permissions removal for a developer
  - Description: "We have a Software Developer who has left their position and we need to have their VPN permissions removed from the Web Group. Their globalId is '_______'."
  - Network Infrastructure Service: Virtual Private Network (VPN)

### Remove SAP Permission with [SAP Security Support](https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=22336)
  - Title: Remove and confirm SAP permissions removal for a developer
  - Description: "We have a Software Developer who has left their position and we need to have their SAP permissions removed. Their globalId is '_______'."

## Tags
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[Office365]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=Office365Tag)