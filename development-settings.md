# How to Access Settings

The preferred method of accessing settings is using built in method calls on base objects. In some cases a developer may need to call the underlying data calls for settings, which bypass caching and are available to all applications regardless if that application is for the web or not. When developing a web application the underlying base calls should not be used, instead the methods available in CMich.Web or CMich.SharePoint should be used. For non-web applications calls can be made from the CMich.Settings assembly.  

## CMich.Web/CMich.SharePoint Settings  

The CMich.Web/CMich.SharePoint assemblies have a set of methods for retrieving/changing user/application settings. The important difference in using methods instead of the CMich.Settings assembly is that settings are cached for 20 minute periods.  All web form and SharePoint applications should use these built in methods and not the CMich.Data methods. The caching is designed to relieve load off the Core API Application database. It is important to let customers who have the ability to change settings know that settings may take up to 20 minutes to take effect.  

## Base Objects  

The CMich.Web and CMich.SharePoint assemblies have a set of base objects that have methods for settings built in. In most cases developer should use these base objects whenever possible. Calls to settings should be done at a high level and not burried inside of a helper or utility class. The base objects are setup to make interacting with the Core API easier and are the preferred route for any calls.

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

### Methods available on Base Objects

*   GetApplicationSettingValue ( CMich.Application, settingKey )

*   Returns the string value for the setting stored in the database. Returns an empty string for settings that are not found.  

*   GetApplicationSetting ( CMich.Application, settingKey )

*   Returns an instance of CMich.Models.Settings.Setting. Returns a NULL for settings that not found.

*   GetUserSettingValue ( CMich.Application, globalId, settingKey )

*   Works the same as GetApplicationSettingValue, but is user specific

*   GetUserSetting ( CMich.Application, globalId, settingKey )

*   Works the same as GetApplicationSetting, but is user specific

*   SetApplicationSetting (CMich.Application, settingKey, value)

*   Attempts to update a setting in the database, if the setting isn't found it is created

*   SetUserSetting ( CMich.Application, globalId, settingKey, value ​)

*   Works the same as SetApplicationSetting, but is user specific

## Non-Base Object Calls

For web applications that do no inherit from base objects developers can make calls directly to the CMich.Web.Settings class, which is a static class. The same methods that are available on base classes are available on this static class with one major difference. Each call has an additional parameter for ApplicationMode. The base objects have the current session available, which defines the current Application Mode. The static class does not have this information, so any calls to the static class will need to get the application mode in some other means.

## CMich.Settings

Inside of the CMich.Settings assembly there is a static class that contains the same methods that are available above in the base objects of CMich.Web and CMich.SharePoint. Just like the static class in CMich.Web these methods require the additional ApplicationMode parameter since the assembly has no way to determine the ApplicationMode  of the current application. The only other difference is this assembly does no do any caching and every call will go to and from the database. Again these methods should not be called unless the application is NOT a web a application.

## Tags
[[Development]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DevelopmentTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
