# ​​​​​​​​Warning  

​The application gateway should be used for testing purposes. If you need an administrative section of your application, you should go down the route of creating a SharePoint group and checking permissiosn that way.  

# ​​​​Adding Application Gateway checks to your application  

1.  <span style="line-height: 1.6;">​Ensure that you have references CMich.SharePoint and other core API pieces in your project  
    </span>
2.  <span style="line-height: 1.6;">You will need to having a using statment for CMich.SharePoint.Utilities so that the extension methods are available for the application gateway</span>
3.  <span style="line-height: 1.6;">Check that the server is not running in production mode, if it is then we do not run any tests for the application gateway since it is not used in production</span>
4.  <span style="line-height: 1.6;">Use the extension method HasTestBedPermission(string username (globalId), string ApplicationId (from the Applications list))</span>
5.  <span style="line-height: 1.6;">If the extension method returns false, end the responds with a meaningful message for the end user</span>

![DevelopingAgainstTheApplicationGateway](/uploads/6d0091003efafe6f1f4eaf498d89896b/DevelopingAgainstTheApplicationGateway.PNG)


## Tags
[[ApplicationGateway]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ApplicationGatewayTag)
[[SharePoint]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SharePointTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
