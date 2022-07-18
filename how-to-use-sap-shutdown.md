## Summary
This article describes how to use the SAP Shutdown functionality from the CoreAPI.

The SAP Shutdown procedure is used when SAP systems are unavailable. The code below shows how to use this functionality. ​
~~~C#
            string message;
            if (CMich.Data.DAL.SapShutdown.SapShutdown.IsSapShutdown(ApplicationMode.Production, out message))
            {
                //SAP is shutdown and message will contain an HTML message to display to users.
            }
~~~

## Tags
[[SAP]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SAPTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)