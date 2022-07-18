## Development

*   ​In development, all CSS must be written in a single LESS file  

*   For development purposes, LESS files must be compiled and the project must use the minified CSS file.
*   In staging, **ALL** custom written LESS files need to be compiled into a single minified CSS file.

*   If the CSS file will be reused on multiple projects, or if used for the styling of templates (such as SharePoint MasterPages and Page Layouts), the compiled CSS files need to be copied over to the CDN at the following location:  

*   For Staging:<span> **\\it-devweb1\WebApplications\api\Static\css\**</span>
*   For Production: <span>**\\it-prodweb1\D$\inetpub\api\Static**</span>  

*   Project files will need to be updated to point to the following location for CSS:

*   For Staging: **http(s)://api2.cmich.edu/static/css**
*   For Production: <span>**\\it-prodweb1\D$\inetpub\api\Static**</span>

## Important Note  

<span>Bootstrap LESS and CSS library files should never be modified. If you feel a modification needs to take place, the issue needs to be raised in a development team meeting. This will ease upgrading of the Bootstrap framework in the future.</span>

[  
](/sites/it/Wiki/HowTo/Design/Pages/home.aspx)

[Back to Design](/sites/it/Wiki/HowTo/Design/Pages/home.aspx)

## Tags
[[CSS]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSSTag)
[[LESS]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=LESSTag)
[[WebDesign]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=WebDesignTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
