# How to SAP like a Novice (WIP)

## Using SAPGUI
1. Launch SAP GUI Logon for **DV4**<br>
    <img src="uploads/665e4c4d3719f73bd47b9594f0379c2d/snip_2022-04-18_09h14m27s.png" width="900">
   <!--![snip_2022-04-18_09h14m27s](uploads/665e4c4d3719f73bd47b9594f0379c2d/snip_2022-04-18_09h14m27s.png)-->
1. Sign in with your Sv4 SAP credentials (not your normal Single-sign-on password)<br>
   >ℹ To setup or reset your SAP Password follow this [KB Article SAP: Changing Own Password](https://cmich.teamdynamix.com/TDClient/664/Portal/KB/ArticleDet?ID=20255)
   <img src="uploads/7fbfb48a8731b222a58079e909997520/snip_2022-04-18_09h15m15s.png" width="900">
1. Selecting your **Transaction-Code** `SE37` (also recommend going into **PRD** SAP and added all the favorite shown in the screenshot for easy reference. If you don't add them in prod they get wiped out each data refreshed, about three times a year)<br>
   <img src="uploads/e5174a532caf1cb91c464e8aed37274c/snip_2022-04-18_09h16m16s.png" width="900">

## Creating Test Data Directory (aka, Variants) as Inputs for RFC Testing
1. Enter your RFC to be tested, **Z...** and click the *wrench* icon<br>
   <img src="uploads/9f10fe75cff3c4b65c78193d2edecab0/snip_2022-04-18_09h18m16s.png" width="900">
1. Enter your desired data **or** select from existing Test Data examples, then click the *clock with the check-mark* to call the RFC<br>
   <img src="uploads/08aebf74de55e051e8af8c183139386f/snip_2022-04-18_09h19m01s.png" width="900">
1. If you see the results you want to share with other, click the *disk* to save the *inputs you used* (note: this does **not** save the results, just the inputs, so others can call the RFC as well. Some RFC calls, such as booking a course, update data, and so calling the RFC without resetting the data will results in different results-you can book a class you are already in, etc.)<br>
   <img src="uploads//bfefaf7fc02936835eba32771affee83/snip_2022-04-18_09h19m25s.png" width="900">

## Tags
[[SAP]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SAPTag)