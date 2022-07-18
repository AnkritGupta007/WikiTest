## Summary
​
<span style="line-height: 22.4px;">The development produced by the web team uses a specific routine that allows information to available on users. This information is stored across all Web Form/SharePoint applications. This pulls so information from SAP and some information from SQL data sources and combines all this information into one object that is of type CMich.Web.Session.Model.SessionInformation. A serialized version of this object is created and stored in a common database that is them retrieved for any further calls against the session. </span>

## How to Access The Session  

The preferred method of accessing the session is using built in method calls on base objects. There may be an occasion where a developer needs to generate a Session object on their own and this can be done with the method CMich.Web.Session.CMichSession.LoadSessionInformation(string globalId or CampusId, ref CMich.Web.Session.Model.SessionInformation sessionObjectToPopulate).  

## CMich.Web/CMich.SharePoint Sessions  

The CMich.Web/CMich.SharePoint assemblies have a set of methods for retrieving the current session. The most important portion to note for a developer, is the developer will need to compile CMich.Web or CMich.SharePoint in the correct application mode. The application mode used by the session is set during a compile condition and will be hard coded after being compiled. There are methods for overloading the applciation mode on the current session, but as a security feature the application mode cannot be changed when it is in Production.  

## Base Objects  

The CMich.Web and CMich.SharePoint assemblies have a set of base objects that have a property built in to retrieve the current user's session. In most cases developer should use these base objects whenever possible. Calls to the current user session should be done at a high level and not burried inside of a helper or utility class. The base objects are setup to make interacting with the Core API easier and are the preferred route for any calls.

### CMich.Web Base Objects

*   MasterPage

*   Page

*   ScriptControl

*   UserControl

### CMich.SharePoint Base Objects

*   Page

*   UserControl

*   WebControl

*   WebPart

*   WebPartPagesWebPart

All of the above base objects have a property named "**CurrentSession**." This will retrieve the current user's session UNLESS the session have been overwritten. Overwriting of sessions is supported for debug purposes, but is not available if the Core API was compiled in Production mode. There are many properties available on the session and developers are encouraged to look at these properties before making calls to other data sources. These properties change some what regularily as the need increases for a particular piece of information.

<span style="line-height: 22.4px;">​​</span><span style="line-height: 22.4px;">\[[</span><span style="line-height: 22.4px;">Documentatio</span><span style="line-height: 22.4px;">n|Back to Documentation</span><span style="line-height: 22.4px;">\]]</span><span style="line-height: 22.4px;">​</span>​​

## Tags
[[Session]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SessionTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)