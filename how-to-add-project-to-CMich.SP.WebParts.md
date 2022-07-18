## ​​​Requirements

*   You must have setup your Vault directory correctly to standard. Please refer to the [Vault Setup](/sites/it/WebTeam/wiki/HowTo/Pages/Vault.aspx) page for more information.

## Creating the Project  

*   Open the solution CMich.SP.WebParts found from the SharePoint2013 directory in your vault working folder
*   Right-Click the solution and Add -> Add New Project
*   Select "SharePoint 2013 - Empty Project"  

*   <span>Name should be the project name you have decided based on the [SharePoint Naming Conventions](Naming-Conventions#SharePoint).</span>

<span>![CreatingWebPartProject](/uploads/3e99285e94254b32f03df2d744775248/CreatingWebPartProject.PNG)  
</span>

*   Click OK
*   On the next step make sure the site you have setup to deploy your project is the URL listed
*   Select "Deploy as a farm solution"

![SelectingServerBlankSolution](/uploads/cbf536b9502c31acfb2d326dd1b076e1/SelectingServerBlankSolution.PNG)

*   Click Finish  

*   Right click on the newly created Project and Select "Properties"
*   Correct the Namespace and Assembly name according to the <span>[SharePoint naming conventions](Naming-Conventions#SharePoint)</span>

<span>![SettingUpAssemblyAndNameSpaceForWebPart](/uploads/8c1158e16c03b6ba8950b238c3c9b1e2/SettingUpAssemblyAndNameSpaceForWebPart.PNG)  
</span>

*   Click on the button "Assembly Information"
*   Switch the "Title" and "Product" fields to match your Assembly Name
*   Set Company to "Central Michigan University"

![SettingAssemblingInformationWebPart](/uploads/8d113d4acf523dba88b59e9b38b35158/SettingAssemblingInformationWebPart.PNG)

*   Click OK
*   Now you should create a feature by right clicking on "Features" in the solution explorer and selecting "Add Feature"
*   Setup your feature according to the [Feature Set Up](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-setup-a-sharepoint-feature) portion of this wiki.

## Tags
[[SharePoint]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SharePointTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
[[Outdated]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OutdatedTag)
