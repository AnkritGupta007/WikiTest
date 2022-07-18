## Description

All SharePoint 2013 Design projects, those that contain branding for the CMich web environment, are housed within CMich.LOD. Following these steps will ensure that you have properly configured a new design project for deployment to the CMich web environment. <span>SharePoint 2013 Design projects should consist of only page layouts, as all sites/pages within the SharePoint 2013 environment will use a single CMich branded MasterPage.</span>  

## ​Requirements

*   You must have created a project in CMich.LOD. Please refer to the [Add Project to CMich.LOD](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-add-project-to-cmich.lod) page for more information.  

## Configuring the Project

### Adding a Module  

*   Page layouts will be housed within a Module inside of the project. To add a Module, right-click on the project and select **Add -> New Item**  

*   <span>Select **Module** and give it a name of **PageLayouts**  
    </span>

<span>![configureDesign1](/uploads/262bf31496cdf93bdffc00f17648909d/configureDesign1.PNG)  
</span>

*   Click **Add**
*   The Module will be added to the project and will contain two files: **Elements.xml** and **Sample.txt**  
    ![configureDesign2](/uploads/cd97cf8b9e58e7521a26e66bf6beed8c/configureDesign2.PNG)
*   For each page layout that is required, copy/paste Sample.txt inside of the Module.
*   Rename Sample.txt (and it's copies) to the proper name for the page layouts. Ex: Assume you are creating the Board of Trustees page layouts. The homepage layout would be called **BOTHome.aspx** and the secondary page would be called **BOTSecondary.aspx**. The page layout name **MUST** include the **.aspx** file extension.  

*   SharePoint will give you wa warning message indicating that a change in the file extension could cause the file to become unusable. This is OK, simply click **Yes** to continue.
*   These newly created/renamed files will house the code for the page layouts.

### Configuring Elements.xml

*   By default, Elements.xml (contained inside of the Module), will pre-poulate with information about the page layouts you've created. This information needs to be heavily modified however.
*   In the **Module** tag, add **Url="_catalogs/masterpage"**
*   In the File tag(s), delete **PageLayouts/** from the Url
*   In the File tag(s), add **Type="GhostableInLibrary"**
*   In the File tag(s), delete the self-closing **/** at the end of the tag, and add a **`</File>`**
*   Between the opening and closing **`<File>`** tag(s), add the following properties:  
    **  `<Property Name="ContentTypeId" Value="0x01010007FF3E05 7FA8AB4AA42FCB67B453FFC100 E214EEE741181F4E9F7ACC43278EE811003A22BFC19B81124C923710F952434E5E" />`**  
    **  `<Property Name="FileLeafRef" Value="Generic1Home.aspx" />`**  
    **  `<Property Name="MasterPageDescription" Value=" Generic 1 Home" />`**  
    **  `<Property Name="UIVersion" Value="15" />`**  
    **  `<Property Name="Title" Value="Generic 1 Home" />`**  
    **  `<Property Name="PublishingHidden" Value="FALSE" />`**  
    **  `<Property Name="PublishingAssociatedContentType" Value=";#$Resources:cmscore,contenttype_welcomepage_name;;#0x010100C568DB52D9D0A14D9B2FDCC96666E9F2007948130EC3DB064584E219954237AF390064DEA0F50FC8C147B0B6EA0636C4A7D4;#" />`**  
    **  `<Property Name="HtmlDesignAssociated" Value="FALSE" />`**  
    **  `<Property Name="ContentType" Value="Page Layout" />`**  
    **  `<Property Name="_ModerationStatus" Value="3" />`**  
    **  `<Property Name="FileDirRef" Value="_catalogs/masterpage" />`**  
    **  `<Property Name="FSObjType" Value="0" />`**
*   The 3 properties that need to be modified are **FileLeafRef**, **MasterPageDescription** and **Title**. 

*   FileLeafRed should match the filename of the page layout
*   MasterPage Description should be a user friendly name of the page layout (spaces are OK)
*   Title should match the Description

### Configuring the Feature  

*   By default, Visual Studio will automatically add a Feature to the project once a Module has been added.  
    ![configureDesign3](/uploads/c12887c713b158af12413b475a64fa40/configureDesign3.PNG)  

*   The feature will be named **Feature1** by default. Right-click on Feature1 and select **Rename**. Rename the feature to the same name that you gave the project. Ex: **CMich.LOD.ProjectName**
*   Double-click on the feature to open it
*   Change the title field to match the name of the Feature (this usually just involves deleting the 'Feature1' text from the title field)
*   In the description field, add the version number, the compiled date, and a brief description of the contents of the project. **Ex:** **Version 1.0.0 - Compiled 5/15/2013 - Contains the Generic 1 Branding Files**
*   Under scope, select **Site**  
    ![configureDesign4](/uploads/d6a84683a9add3c6e9466806bd63221a/configureDesign4.PNG)
*   The last step is to set the Image Url for the Feature. This is an image that will display within SharePoint to denote that this is a custom CMU developed feature. With the Feature still open, find the **Image Url** property in the Properties pane in the lower right of Visual Studio
*   Add the following to the Image Url: **CMichCoreAPI\CMichMOSS.png**

## Tags
[[SharePoint]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SharePointTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
