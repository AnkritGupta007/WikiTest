## ​​​Code/Design reviews  

All projects s​​ho​uld receive code and​ design reviews(s). Code reviews will assess the project from a development perspective, mainly the code behind, database, advanced JavaScript UI and organization of the project itself. Design reviews will assess the project from an overall user interface/experience and accessibility perspective. In both review types reviewers will use the documentation laid out in this wiki as a guide to what to fix. ​

Small and extra small projects (refer to [DevReq ](https://apps.cmich.edu/devreq/) for project size definitions) will be required to have a minimum of one code and one design review. Any project that is medium or larger with require a minimum of two code and two design reviews. One of each at the beginning and one of each at the end. If the reviews at the beginning reveal that the project is following all standards and has little to no problems, there will not be another review until the project goes into UAT. If the project goes into UAT multiple times, a review should be performed for each time that features are added.​

## Projects with an upgrade to an existing database

<div>​Any project that requires a database upgrade the following is expected  
</div>



<div>

*   At the start of a project a copy of the production database should be made for development purposes
*   An upgrade script should be created to upgrade the database, no manual changes should be needed outside of the upgrade script
*   Whenever the upgrade script is created/modified and the project goes into UAT, the developer should copy the database from production and apply their change script it. The upgraded production database should be used for UAT. 

</div>

## Tags 
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[Database]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DatabaseTag)
