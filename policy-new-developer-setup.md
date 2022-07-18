# New Developer Setup
This page documents all information and setup required for a new developer, with links to more specific documentation where appropriate. This is the master guide for new hire setup, training, and resources.

## Setup Checklist
### Prior to Start Date
* Get workstation imaged/purchased or vm Desktop setup
  * **Direct Hires:** Usually get a laptop and dual monitors setup in the office
  * **Students:** We usually have an old PC and dual monitors and a VM Desktop
     - Ticket for VDI with [Developer Virtual Desktop Request](https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=22357)
        - Title: Add student developer to it-vdi-developers-users and their it-account as admin on their virtual machine
        - Description: "We have a new student software developer who needs to have a VM assigned to them, 'it-vdi-dev__'. Please also add their it-globalId account to the VM as an admin so they can install and update tools like Visual Studio. Their globalId is '_______'.
  * **Contractors:**
    * Add `IT-AppDevelopment-Contractor-Admin` to the Administrator role on the workstation 
    * Add `IT-AppDevelopment-Contractor` to the [Remote Desktop Users](How-to-add-permission-to-remote-in-to-your-dev-machine) on the workstation 
* Get Global ID
    * Add to AD Group depending on type of hire: (all group is within `IT-AppDevelopment`) 
        * **Students:** Add to `IT-AppDevelopment-Student` (it-whitm1ek must add)
        * **Direct Hires:** Add to `IT-AppDevelopment-Staff` (it-whitm1ek must add)
        * **Contractors:** Add to `IT-AppDevelopment-Contractor` (it-whitm1ek must add)
    * Setup Microsoft Teams and Outlook
      - Access to https://centralmichigan.sharepoint.com/sites/ApplicationDevelopmentTeam (Member Access)
      - Access to https://centralmichigan.sharepoint.com/sites/EnterpriseSoftwareDevelopment931 (Member Access)
        - Add to Outlook groups at https://outlook.office365.com/people/group/groups.cmich.edu/applicationdevelopmentteam
          - ApplicationDevelopmentTeam@groups.cmich.edu
          - EnterpriseSoftwareEngineering@groups.cmich.edu
    * Setup Gitlab Permissions (This should be autoset by AD group, but go check)
        * https://code.cmich.edu/groups/IT-AppDevelopment/-/group_members and add them as a Maintainer
        * **Students:** Should be added as a Developer rather than a Maintainer.
    * Add to Dev Team/Dev Student Outlook Group
    * Add to Bi-Weekly Team Meeting
* Get [TDX Setup](https://cmich.teamdynamix.com/TDClient/Requests/ServiceCatalog?CategoryID=8318)
    * In User Setup Request mention "Configure user to have IT-AppDevelopment notifications turned off"
    * Set default desktop
    * Request access to TDX-Sandbox as well
    * **Contractors:** Fill out [form](https://cmich.teamdynamix.com/TDClient/Requests/ServiceDet?ID=14930) Title Add "Development & Maintenance > Workspace time" Time Type for {contractor name and gid}"


### First Day
* New student/direct hires must go to HR on their first day
* Tell them to fill out https://healthscreen.apps.cmich.edu daily
  * Tell them to read https://www.cmich.edu/covid19/Pages/Health-Safety-Protocols.aspx#guidelines about mask wearing guidelines
  * Remind them that they will need weekly tests until 2 weeks after being fully vaccinated https://www.cmich.edu/covid19/Pages/Protect-yourself-Protect-others.aspx 
  
* Setup IT Account via [Active Directory Management Ticket](https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=15012)
  * Title: "IT Account setup for developer"
  * Description: "We have a software developer who has joined our team and we need to have their it-globalId account setup. Their globalId is '_______'."
  * **Students:** Mention in the Description "They are a student developer and need to be added to `\\IT-STORM\IT-StuEmp$\StudentEmployees.txt`."
* Add IT Account to proper IT Admin group accounts to have admin rights on the computer or vm
    * **Students:** Add IT Account to `IT-AppDevelopment-Student-Admin` (it-whitm1ek must add)
    * **Direct Hires:** Add IT Account to `IT-AppDevelopment-Staff-Admin` (it-whitm1ek must add)
    * **Contractors:** Add IT Account to `IT-AppDevelopment-Contractor-Admin` (it-whitm1ek must add)

#### Setup computer
* Get password setup
* Setup IT Account Password with [IT Account KB Article](https://cmich.teamdynamix.com/TDClient/664/Portal/KB/ArticleDet?ID=35382)
* Confirm IT Account has Admin rights on their computer or VM (VM might have admin rights with a normal global)
* Install needed software from [Software Center](https://cmich.teamdynamix.com/TDClient/664/Portal/KB/ArticleDet?ID=20301)
    * Web Browser of choice (Firefox/Chrome)
    * Office 365
    * Microsoft Teams
    * SAP Business Explorer
    * SAP GUI for Windows
    * VOIP Client - Cisco Jabber
    * Remote Desktop Connection
    * VPN
       * Primary - [GlobalProtect (Palo Alto) VPN Client](https://cmich.teamdynamix.com/TDClient/664/Portal/KB/ArticleDet?ID=36303)
       * Backup - AnyConnect VPN Client ([Available here for personal devices](https://www.cmich.edu/office_provost/OIT/Download/Pages/default.aspx))
    * Any other desired apps or tools should be installed from the Software Center rather than online (if available)
* Install [NotePad++](https://notepad-plus-plus.org/download)
* Install [NodeJS LTS](https://nodejs.org/en/download/)
* Install [Windows GIT](https://git-scm.com/download)
* Install [VS Code](https://code.visualstudio.com/)
* Install [SQL Server Management Studio 18](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)
* Install Visual Studio - [VS 2019 PRO](https://visualstudio.microsoft.com/downloads/) (We no longer use license keys for VS, we instead any Team Lead adds them to `IT-AppDevelopment-VisualStudio` for our site license)
    * [x] **ASP.NET and web development** Workload
    * [x] **.Net Framework 4.8 SDK** individual component
    * [x] **TypeScript 4.3 SDK** individual component
    * [x] **GIT for Windows** individual component
    * [Web Essentials 2019](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebEssentials2019)
    * [Add the CMU NuGet Repository](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/-/wikis/how-to-add-the-cmu-nuget-repository-to-visual-studio)
* Install [ReSharper](https://marketplace.visualstudio.com/items?itemName=JetBrains.ReSharper) - need product key from Eric Whitmore
* Install [SAP .dll files](How-to-Install-Missing-SAP-dlls)
* Install [TypeScript 2.9.2](http://download.microsoft.com/download/7/0/A/70A6AC0E-8934-4396-A43E-445059F430EA/2.9.2-TS-release-dev14update3-20180612.2/TypeScript_SDK.exe) (maybe no longer needed -Eric J)
* Install [KeePass 2](https://keepass.info/download.html)
    * Database Location: `\\cab\appdev$\keepass\AppDev.kdbx`
    * Database Password: `fireupchips`
* Printer Setup [ricoh-readme.rtf](/uploads/bab131f2920dfc79fd7dfa80f2430d17/ricoh-readme.rtf)
    * TODO: Create and add documentation for printer locations
* Setup [Outlook Calendar Permissions](Calendar-permissions-policy)

## Expectations
* **Students:** Read [Student Expectations](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/-/wikis/Student-Expectations)
* Read [OIT Self Expectations](https://centralmichigan.sharepoint.com/sites/oit/Shared%20Documents/Forms/AllItems.aspx?FolderCTID=0x012000D8BBB37BCCE26A49B77BED17A3CB6872&id=%2Fsites%2Foit%2FShared%20Documents%2FGeneral%2FOIT%20Official%20Documents%2FOIT%20Team%20Expectations%2Epdf&parent=%2Fsites%2Foit%2FShared%20Documents%2FGeneral%2FOIT%20Official%20Documents)

## Training
* Documents
    * LSI - https://www.cmich.edu/office_president/Documents/leadershipstandards_poster.pdf
    * [OIT_Team_Expectations.pdf](/uploads/80cb9e50878520251e49a3be36a3f7aa/OIT_Team_Expectations.pdf)
* TDX Training
  * [KB Article - ITSM: Service Level Agreement (SLA) Impact, Urgency, and Priority Matrix](https://cmich.teamdynamix.com/TDClient/KB/ArticleDet?ID=35894)
  * [How to request a change calendar deployment](how-to-request-a-change-calendar-deployment)
  * See a team lead for further training if needed
* Git/Gitlab Training (ask a team lead for overview)
  * [Our Current GIT Branching Strategy](policy-git-branching-strategy)
* Provide Outlook training if needed
* Setup ADA training
  * [Accessibility](Accessibility)
  * [General Web Accessibility](general-web-accessibility)
  * [Accessibility Tools](accessibility-tools)
* Read [Enterprise_Stack_forCMU_by_Eric_Whitmore_2017.pptx](uploads/fa35d9792ca7bf0b23664a50c2ffed68/Enterprise_Stack_forCMU_by_Eric_Whitmore_2017.pptx) Presentation
* Read [clean_code.pdf](/uploads/d958bf2c9bc66225b36f8e4e99e8b509/clean_code.pdf)
* Read [Art of Unit Testing](training-material-unit-and-integration-testing)
* Read [What .NET Developers ought to know to start in 2017](https://www.hanselman.com/blog/WhatNETDevelopersOughtToKnowToStartIn2017.aspx) as an overview. (Note: You can skim without drilling down into every link and read all the details at another time.)

## Tags
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[VisualStudio]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=VisualStudioTag)
[[VSCode]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=VSCodeTag)
[[Notepad++]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=Notepad++Tag)
[[Office365]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=Office365Tag)
[[Training]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TrainingTag)