# Summary
Deploying to SharePoint is a join effort between the AppDev team and the AppSupport team.  This document outlines the process for deploying SharePoint code to production.

This specifically details this process from the perspective of the AppDev team.

## Process Overview
1.  Develop on local machine
2.  Deploy to Test (Beta/Res) Environment
3.  Deploy to Staging
4.  Schedule Release
5.  Deploy to Production

### Develop on local machine
1.  Development Servers
    * `OC-SP2013`
      * Set working directory to "E:\Projects\GitLab"
    * `it-sp13-d-app1` / `it-sp13-d-app2` / `it-sp13-d-app3`
      * Set working directory to "C:\src\GitLab"
2.  Once coding is finished, publish by right clicking on the project's name and selecting "Publish...".  

***Note***: If updating the SharePoint Core API, you will need to change the build configuration for each environment.  (The .wsp file can be renamed to .cab to verify the contents are correct).



![publish](/uploads/27bbe0f2ac3df05d51f604cca49303d4/publish.png)  
3.  Then save the package to your local machine, not the server 
	* UDrive is convenient since changes will be available on remote servers and local computer (See [Mapping UDrive](https://cmich.teamdynamix.com/TDClient/KB/ArticleDet?ID=20373)) 

![publish2](/uploads/6de03e59523adf72ed319bda3bdd3a7a/publish2.png)  


### Deploy to Test (Beta/Res) Environment
1.  Remote in to the Res/Test Server
    * `IT-RES13APP2`
2.  Developer puts package into the Deployments folder with the current date:
    * Use Remote Desktop Connection to connect to server.
    * D:\1-Deployments\YYYY-MM-DD
	    * If folder already exists, make \YYYY-MM-DD-old and add old files there.
	    * Then put new .WSP file in the \YYYY-MM-DD
    * Double-click `D:\1-Deployments\Deploy-SolutionByTimestamp.bat` to Run PowerShell script `Deploy-SolutionsByTimestamp.ps1`
       * Close the PowerShell IDE that pops-up
    * The CMD Window will auto-close when done, and this can take a few minutes
    * If deployment fails (either in Powershell or in Betaweb)... search for most recent version of the deployed .WSP and run the script on the old .WSP to revert the changes.
3. Verify changes have successfully been made on the test environment by loading the Betaweb version of the page.
    * Betaweb version typically replaces the "www" in the web address with "betaweb". 
      * (ex. https://betaweb.cmich.edu/Pages/Default.aspx)
4. If changes to CSS or Javascript are made on the project, a CDN deployment will potentially need to be done.
    * Test/Staging CDN is found at '\\\\it-stgcdn01\\cdn'.
    * Files are copied over 

### Commit Changes to GitLab and Conduct Code Review
1. If changes are not already on GitLab, create a branch and commit changes to that branch.
    * Make sure before changes are added to staging and the Scheduling 

### Deploy to Staging
1.  Developer puts the same package/WSP into the Deployments folder:
    * `\\SP-stgapp02\Deployments\To Be Deployed`

***Note***: If updating the SharePoint Core API, you will need to change the build configuration for each environment.  (The .wsp file can be renamed to .cab to verify the contents are correct).

### Schedule Release
1.  Go through [How to request a deployment](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-request-sharepoint-deployment)

### Deploy to Production
1. This is done by the AppSupport team whenever that team can get it done. Once the change is completed the original ticket that requested the change must be updated and resolved.
    * Change window is typically Thursday Morning (12:00 a.m. - 6:00 a.m.)

## Other Gotchas

### "The name 'InitializeControl' does not exist in the current context"

### Docs
[SharePoint_Deployment_-_Developer_Edition.pdf](/uploads/57de7f7d0fb7ef7d040291c7bbb0b8f9/SharePoint_Deployment_-_Developer_Edition.pdf)

## Tags
[[SharePoint]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SharePointTag)