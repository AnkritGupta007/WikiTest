## ​Introduction

​Our servers are set up in a "cluster." We currently push all applications to one server and then the data is pushed to other servers through a linked file system. In the event that one server goes down another server takes control of everything. In the event that this happens we would like to know that our publish is going to the correct server. We would also like to know in the event that a server gets decomi​​ssioned what server we are publishing to. We can just look at the publish profile, but instead of that we would like a consistent naming convention for publish profiles.  

## Convention  

​Please ensure that the server name and application mode are in the name for your publish profile.  

If you are using our standard servers and application modes the publish would look like the following:

[PublishProfile](/uploads/76fecd6e97cc2d485e81947008f84d4b/PublishProfile.PNG)

## Tags
[[Conventions]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ConventionsTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
