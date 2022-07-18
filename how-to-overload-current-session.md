​​​The current web form/SharePoint applications have a Current Session object associated to base objects that allows for standard data to be retrieved on a user. You can read more about this at the [Developer Session](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-development-session) section of this wiki.  

<span>

By default the current session available through the API only supports the current user who is logged in based on the security model of the application. Generally this means it uses whatever user has authenticated with NTLM security. <span><span>As developers we often need to run tests against the code we develop. To allow for testing to occur as a different user there is a method built into the CMichSession object that will override CurrentSession on all base objects with another user and/or a different application mode. The one exception to this, is the method will not allow a user to switch a Production session to another user. This is a security feature and developers should not work to try to bypass this.</span></span>

Developers can use the following method to change the "CurrentSession" object that is available as a property on all base objects.  

CMich.Web.Session.CMichSession.SetAlternativeSession(string globalID or CampusId, CMich.ApplicationMode applicationMode)

## Precauations

</span>

*   As stated above when an application is in Production mode the above method will not work
*   Once a session is over loaded it will remain overloaded as long as the current session (cookie driven) is active
*   The above method should only be used in a debug session and should never appear in production level code
*   If you are calling CMich.Web.Session.CMichSession.ServerApplicationMode this will not be overwritten by using the above method and will always be what is compiled with the CoreAPI build mode.

## Tags
[[Session]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SessionTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)