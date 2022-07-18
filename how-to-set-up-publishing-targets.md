## Summary
This article explains how to setup publishing targets within Visual Studio and on the destination server.

​There are 3 publishing targets that exist within our environment. These include:

*   Development: it-resweb01  

*   Staging: it-stgweb01
*   Production: it-prdweb01

To setup the publishing targets for a project on the destination server:

1.  Remote into the destination server.
2.  Open IIS Manager
3.  In the "Connections" pane on the left, expand "Sites -> apps.cmich.edu".
4.  Right-click on "apps.cmich.edu" and select **Add Application**.
5.  In the "Add Application" dialog box, enter the name of the application in "Alias". (Ex: TuitionWaiver)
6.  Under "Application pool", select **IT-DMU 4.0 Integrated**.
7.  In "Physical path", navigate tothe folder located at D:\inetpub\apps\APPLICATION_NAME (You will need to create the folder for the application in this location).
8.  Click "OK".
9.  Repeat steps 1-8 until each of the 3 servers indicated above have been configured.  

To setup these publishing targets within a project for Visual Studio:

1.  From the Visual Studio menu, click **Build -> Publish**.
2.  From the "Publish Web" dialog box, select the "Profile" option and click "Custom".
3.  Enter **it-resweb01 - Development** and click "OK".  

4.  Under "Publish method", select **File System**.
5.  Under "Target location", select the forlder on that server. (Ex: \\it-resweb01\D$\inetpub\apps\APPLICATION_NAME)
6.  Click "Publish".
7.  Repeat steps 1-6 for each of the 3 environments, entering **it-stgweb01 - Staging** and **it-prdweb01 - Production** for Step 3 when needed.

## Tags
[[Conventions]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ConventionsTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)