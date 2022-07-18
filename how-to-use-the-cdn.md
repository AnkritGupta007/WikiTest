# Summary
The CDN (Content Delivery Network) should be used for serving files related to front-end frameworks, fonts, and images that are used across applications and websites. Typically, we avoid using other's CDN's or public CDN's as we cannot guarantee the content will always be available. We host files such as Bootstrap, jQuery, CMich Icons font, Oxygen and Roboto Slab, among many others.

Do not put content on PRD until it has been tested on STG.

## Locations:

| **Location** | **Path** | **URL** |
| :---: | :---: |:---: |
|Staging CDN | `\\it-stgcdn01\cdn` | https://stgcdn.cmich.edu/ |
|Production CDN | `\\it-prdcdn01\cdn` | https://cdn.cmich.edu/ |

## Update code in Gitlab Repo
- Please also update code you add the the prod network folder to https://code.cmich.edu/IT-AppDevelopment/CustomApplications/CMichCDN as well

## Tags
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[Git]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=GitTag)
[[CDN]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CDNTag)