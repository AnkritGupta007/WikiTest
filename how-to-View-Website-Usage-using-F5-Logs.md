# Summary
There are times when it is helpful to know if or how web applications are utilized.  F5 usage logs can be searched using CMU's Elastic server (sometimes referred to as "ElStack") to learn about traffic and if certain URLs are being hit, if so what type of traffic or requests are coming in.

You can access the [Elastic Server](https://it-el1-kib1:5601/app/home#/) generally or jump into a direct link to the [F5-2-http-* Logs](https://it-el1-kib1:5601/app/discover#/?_g=(filters:!())&_a=(columns:!(),filters:!(),index:dd424270-ed5d-11ea-9078-435507025d2b)).

## Logging into The F5 Elastic Server
Login credentials are stored in KeePass under **AppDev** > **Other** > **CMU Elastic Search Login**.

![image](uploads/44fe71a935d58edac69dc34778db5824/image.png)

<!--
![Main Page](uploads/e3d8b0240f3d034f6e0e7eb124e87454/image.png)

![Menu](uploads/827e167ad8f5c482abdb320de9431330/image.png)

![Select F5-2-http-*](uploads/ceb54def93c4767aa48ebbc0abd3cdd8/image.png)
-->

## Filtering the F5 Logs
![F5-2-http-* Default View](uploads/5422b31d2d6f51913868b850e5f83ef5/image.png)

The default view does not include any filtering and shows information for the last 24 hours (including traffic from within the last few seconds).

Free text searches are supported, but using [Kibana Query Language](https://www.elastic.co/guide/en/kibana/current/kuery-query.html#_boolean_queries) will provide more accurate results.  The example below searches for requests to "https://apps.cmich.edu/FirstImpressions/" with a return code of 200.  Note that one must used to correct search box on the page.  
<!--![Search](uploads/3a0dab5aa723c70e8454bce6cc837ced/image.png)-->
![image](uploads/0f6711a0900c2e54576b60992914aa21/image.png)

One can also set the data ranges:  
![Date Ranges](uploads/bbb3eeb685934ca1639604cc4a72901a/image.png)

Clicking the disclosure triangle ">" will show more detailed information for a given result.  
![image](uploads/03330d17a254d8661499a6189264909b/image.png)
