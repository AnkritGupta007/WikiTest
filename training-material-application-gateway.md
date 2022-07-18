# ​​​​​​​​​​​​​​URLs for Different Test Systems  

*   ​​​​Research  
    <span style="color: #262626; font-family: &quot;segoe ui semilight&quot;, &quot;segoe ui&quot;, segoe, tahoma, helvetica, arial, sans-serif; font-size: 1.15em; line-height: 1.4;">-</span> [https://betaweb.cmich.edu/_layouts/applicationgateway/default.aspx](https://betaweb.cmich.edu/_layouts/applicationgateway/default.aspx)<span style="color: #262626; font-family: &quot;segoe ui semilight&quot;, &quot;segoe ui&quot;, segoe, tahoma, helvetica, arial, sans-serif; font-size: 1.15em; line-height: 1.4;">​ - Application Gateway  
    </span><span style="color: #262626; font-family: &quot;segoe ui semilight&quot;, &quot;segoe ui&quot;, segoe, tahoma, helvetica, arial, sans-serif; font-size: 1.15em; line-height: 1.4;">- </span>[https://betaweb.cmich.edu/_layouts/15/people.aspx?MembershipGroupId=69150](https://betaweb.cmich.edu/_layouts/15/people.aspx?MembershipGroupId=69150)<span style="color: #262626; font-family: &quot;segoe ui semilight&quot;, &quot;segoe ui&quot;, segoe, tahoma, helvetica, arial, sans-serif; font-size: 1.15em; line-height: 1.4;">​ - SharePoint Group  
    </span><span style="color: #262626; font-family: &quot;segoe ui semilight&quot;, &quot;segoe ui&quot;, segoe, tahoma, helvetica, arial, sans-serif; font-size: 1.15em; line-height: 1.4;">- </span>[https://betaweb.cmich.edu/Lists/ApplicationGateway_Permission/AllItems.aspx](https://betaweb.cmich.edu/Lists/ApplicationGateway_Permission/AllItems.aspx)<span style="color: #262626; font-family: &quot;segoe ui semilight&quot;, &quot;segoe ui&quot;, segoe, tahoma, helvetica, arial, sans-serif; font-size: 1.15em; line-height: 1.4;">​ - Permission List  
    </span><span style="color: #262626; font-family: &quot;segoe ui semilight&quot;, &quot;segoe ui&quot;, segoe, tahoma, helvetica, arial, sans-serif; font-size: 1.15em; line-height: 1.4;">- </span>[https://betaweb.cmich.edu/Lists/ApplicationGateway_Applications/AllItems.aspx](https://betaweb.cmich.edu/Lists/ApplicationGateway_Applications/AllItems.aspx) <span style="color: #262626; font-family: &quot;segoe ui semilight&quot;, &quot;segoe ui&quot;, segoe, tahoma, helvetica, arial, sans-serif; font-size: 1.15em; line-height: 1.4;">- Application List</span>

*   <div>Staging  
    - <a>https://stgweb.cmich.edu/_layouts/applicationgateway/default.aspx​</a> - Application Gateway  
    - [https://stgweb.cmich.edu/_layouts/15/people.aspx?MembershipGroupId=71811](https://stgweb.cmich.edu/_layouts/15/people.aspx?MembershipGroupId=71811) - SharePoint Group  
    - [https://stgweb.cmich.edu/Lists/ApplicationGateway_Permission/AllItems.aspx](https://stgweb.cmich.edu/Lists/ApplicationGateway_Permission/AllItems.aspx) - Permission List  
    - [https://stgweb.cmich.edu/Lists/ApplicationGateway_Application/AllItems.aspx​](https://stgweb.cmich.edu/Lists/ApplicationGateway_Application/AllItems.aspx) - Application List  
    </div>

# Differences in Systems  

​Most users should do their testing in the staging environment. All environments can be changed to any of the SAP servers through the application gateway, so you do not need to be on the staging server to get to the staging SAP environment. The staging environment will be the environment with the closest code/content as production and receives updates for QA testing only. The research server is often updated many times a day with code that is not ready for end user testing.​  

# Adding a New User  

1.  <span style="line-height: 1.6;">Add the user to the SharePoint group by using the "SharePoint Group" link from the above list for the test system you are giving the user access to. </span>  

2.  <span style="line-height: 1.6;">Add a new item to the "Permission List" link</span>
3.  <span style="line-height: 1.6;">Select each application the user should have access to</span>

<div><span style="line-height: 20.8px;">The user should now have permission immediately</span></div>

## ​​​​Changing a User's Permission to Applications​  

1.  ​Find the user on the above link "Permission List" for the test system you want to change permission on
2.  ​Check or uncheck different applications for the user

​​​​​​​As soon as you save the item the user will have the new permissions immediately.  

# ​​Adding new Application to the Gateway  

1.  ​​First add a new item to all the application lists located at the above "Application List" links  
    - The **ApplicationId** is a unique identifier for the application, which should contain no spaces or special characters.   
    - The URL field will contain a link to the application and text to display in the application listing on the Application Gateway  
    **For each of the "Permission List"s listed above, do steps 2 through 4**  

2.  <span class="ms-rteThemeForeColor-1-0">​</span>Navigate to the list, expand the ribbon (if it isn't) and select "List Settings"  
    ​![RibbonListSettings](/uploads/3ce21aa30155e7e16c09a64f0f819432/RibbonListSettings.PNG)
3.  Select "Add Column" under the list settings  
    ![CreateColumn](/uploads/f96ca3ef5c959a0af808fb53e59096e8/CreateColumn.PNG)  

4.  To create the new column do the following  
    - Enter the **ApplicationId** you selected when adding the application to the "Application List"  
    - Select "Yes/No (check box)" as column type  
    - Set the "Default Value" to "No"  
    ![AppGateway_AddNewColumnToPermissionList](/uploads/d10b3cef7dd73d2495262fd09953b9cb/AppGateway_AddNewColumnToPermissionList.png)  

5.  ​​Once the new item is added you can add the permission to specific users by using the information provided above under "Adding a New User" and "Changing a User's Permission to Applications"  

</div>

## Tags
[[ApplicationGateway]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ApplicationGatewayTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
