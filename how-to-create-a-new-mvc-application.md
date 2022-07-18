## Information

​This documentation was created using Visual Studio 2013, but 2015 should be the same process. We will evaulate this documentation when new versions come out.  

## ​Steps

1.  <span style="line-height: 1.6; display: inline;">​​Go to File -> New Project</span>  

2.  <span style="line-height: 1.6; display: inline;"><span style="font-size: 10.5pt; font-family: arial, sans-serif; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">Select Templates -> Visual C# -> Web -> ASP.NET Web Application (for Location choose your Vault Folder, e.g. C:\Projects\Solutions\Web Applications)</span>  
    ![SelectProject](/uploads/d4ad9d082e0e4e49ed1eecbf74183ca8/SelectProject.PNG)</span>
3.  <span style="line-height: 1.6; display: inline;"><span style="line-height: 1.6;">Select Empty and check the MVC checkbox  
    </span>![EmptyMvc](/uploads/098e84413d9e787e7f8a7583d1f82f84/EmptyMvc.PNG)  
    </span>
4.  <span style="line-height: 1.6; display: inline;"><span style="line-height: 1.6;"> Rename "Models" folder to "ViewModels  
    ![RenameViewsFolder](/uploads/0538ada061c37f894a32fe8c7c86b001/RenameViewsFolder.PNG)  
    </span></span>
5.  <span style="line-height: 1.6; display: inline;"><span style="line-height: 1.6;">Get latest version from vault for the project Designs -> CMich.ApplicationTemplateBootstrap3MVC  
    </span></span>
6.  <span style="line-height: 1.6; display: inline;"><span style="line-height: 1.6;">From the root of the project CMich.ApplicationTemplateBootstrap3MVC copy the folder Scripts and the file Packages.Config into your project  
    ![Root_To_Copy_From_ApplicationTemplate](/uploads/594d13364d99722194887259e7842710/Root_To_Copy_From_ApplicationTemplate.PNG)  
    </span></span>
7.  From the "Views" folder of the project ​<span style="line-height: 22.4px; display: inline;">CMich.ApplicationTemplateB</span><span style="line-height: 22.4px; display: inline;">ootstrap3MVC c</span><span style="line-height: 22.4px; display: inline;">opy the folder "Shared" and the file "_ViewStart.cshtml" to the "Views" folder of your application  
    ![Copy_From_Views](/uploads/75b5fc56a9da6bfeb5d2a533a81db6c7/Copy_From_Views.PNG)  
    </span>
8.  Go to Project -> YOUR_PROJECT Properties and select the Application tab
9.  If your Target framework is not set to a minimum of NET Framework 4.5.2 change this dropdown to reflect that  
    ![Change_to_4.5.2](/uploads/1ebd3585fda5e80f513b720ac13ac5d2/Change_to_4.5.2.PNG)  

10.  Go to Tools -> Nuget Package Manager -> Package Manager Console
11.  Run the command "update-package​ -reinstall" This will install our default Nuget packages  
    ![ReinstallNuget](/uploads/3d4e981ea33de2c7d2fa6676c64c6bcd/ReinstallNuget.PNG)  

12.  Right click on the Solution​​​ ​(it is important that this is the solution NOT the project) and select “Add to Vault”​
13.  <span style="font-size: 10.5pt; font-family: arial, sans-serif; background-image: initial; background-attachment: initial; background-size: initial; background-origin: initial; background-clip: initial; background-position: initial; background-repeat: initial;">Right click on the Solution  -> Add -> Existing Project… , and from CMich API repeat for each of the following: CMich, CMich.ConnectionSettings, CMich.Data, CMich.Logging, CMich.SAP, CMich.Security, ​CMich.Settings, CMich.Web, CMich.Web.Mvc, CMich.WebServices​</span>![CoreAPIProjects](/uploads/0dbe4d28900441d745803695ab5d2bd7/CoreAPIProjects.PNG)  

14.  Add a reference to each of these projects to your project  
    ![AddReferences](/uploads/09a6b5aaad0f7161802440814a4e8c8a/AddReferences.PNG)  

15.  Replace "Application Title" with your application's title inside of Views -> Shared -> _layouts.cshtml  
    ![RenameApplicationName](/uploads/8ddf3643f95c85aadb257337e65de307/RenameApplicationName.PNG)  

16.  Your project is now created. After this refer to the how to article [Using MVC Base Objects](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/cmich-web-mvc)

## Tags
[[MVC]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=MVCTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
