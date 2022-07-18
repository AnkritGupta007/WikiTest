## ​​Requirements

*   SharePoint Server 2013 - In order to create a SharePoint 2013 Solution, you must be working on a machine that has SharePoint 2013 server installed and running.
*   Visual Studio 2012 - Visual studio 2012 will be needed for creating the solution. You must also have the Office Developer Tools for Visual Studio 2012 and the SharePoint Client Components installed. You can find these at [http://msdn.microsoft.com/en-us/office/apps/fp123627](http://msdn.microsoft.com/en-us/office/apps/fp123627)
*   Vault - You will need Vault setup to our configuration. You can find out more information at the [Vault Setup](/sites/it/WebTeam/wiki/HowTo/Pages/Vault.aspx) page.  

*   SharePoint Naming Conventions - Know the [SharePoint naming conventions](Naming-Conventions#SharePoint) for projects
*   SharePoint Site - A site on the local SharePoint instance where you can deploy your solution  

## Creating Solution

*   Open Visual Studio 2012
*   Select File -> New -> Project
*   Select SharePoint 2013 - Empty Project
*   Name should be the solution name you have decided based on the [SharePoint Naming Conventions](Naming-Conventions#SharePoint)
*   Location will be <YOUR_VAULT_DIRECTORY>\Solutions\SharePoint2013

![CreatingBlankSolution](/uploads/0e6cb6bf1116ac436835f022adfc7527/CreatingBlankSolution.PNG)

*   Click OK
*   On the next step make sure the site you have setup to deploy your project is the URL listed
*   Select "Deploy as a farm solution"

![SelectingServerBlankSolution](/uploads/862ea1c760f7bfc9d20226de3fc4c14f/SelectingServerBlankSolution.PNG)

*   <span>Click Finish</span>
*   Right click on the newly created Project and Select "Properties"
*   Correct the Namespace and Assembly name according to the <span>![SettingUpAssemblyAndNameSpace](/uploads/a123f480e3ff92c7a2dfa6ac39cb4076/SettingUpAssemblyAndNameSpace.PNG)</span>


*   Click on the button "Assembly Information"
*   Switch the "Title" and "Product" fields to match your Assembly Name
*   Set Company to "Central Michigan University"
*   Click OK
*   Now you should create a feature by right clicking on "Features" in the solution explorer and selecting "Add Feature"
*   Setup your feature according to the [Feature Set Up](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-setup-a-sharepoint-feature) portion of this wiki.

## Tags
[[SharePoint]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SharePointTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
