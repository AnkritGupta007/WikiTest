## Entering a New Redirect in Prod

## When a WebDirector Redirect is NOT What You Want
WebDirector does not work for items that live outside SharePoint (such as externally hosted apps).  CMich URLs for externally hosted apps can be accomplished by a DNS CNAME record, but that’s typically done by App/Networking and may require coordination with the vendor that provides the app.

## Steps for Making a New Redirect in Webdirector
Most of the time you do not need to add a new subdomain (aka, **Path**) so you can skip step **1) Build the **Path** (i.e., subdomain)** and step **2) Request to Networking for a DNS Entry Point**

1. Build the **Path** (i.e., subdomain)
   > ℹ A **Path** or **Path URL** in WebDirector is actually a subdomain which is linked to a **Group** of people  (see below) who could manage redirects within that subdomain. 
   - Go to https://apps.cmich.edu/WebDirector > Admin > Paths
   - Click **Create new path** and enter your value (in our example `archive2.cmich.edu`)
   - Pick a **Group** (in our example, `OIT`). 
     > ℹ The original idea was the group would owns it and manages it, but Kole Taylor, It_APPLICATIONS or IT_APPLICATION_DEVELOPMENT are practically the managers for all.
   - Click **Create Path**
1. Request to Networking for a DNS Entry Point
   - Note the IP address of WebDirector: 35.33.64.44 (you can verify this with `ping astra.cmich.edu`) 
   - Send in TDx Service [Request ticket to Networking](https://cmich.teamdynamix.com/TDClient/664/Portal/Requests/ServiceDet?ID=22329), Description "Please put in a DNS entry for `archive2.cmich.edu` to point at `35.33.64.44` for a new WebDirector entry."
1. Add Individual Redirect URL
   - Add Redirect, click *Create New Redirect*
   > ⚠ A **Short URL** is  a **Path/subdomain** combined with a subdirector/folder path. 
   - Pick **Short URL** **Path** that already exists or that you created in Step 1 above and enter your desired subdirector/folder path (e.g., `/my/desired/sub/director.aspx`) in the second field.
     > ⚠ If you have no specific subdirector, you should still enter a "/" in the field to the right of the drop-down **Path**, as this avoids some kind of errors.
   - Enter the **Destination URL** users should be directed to 
   - In **Requested By** add your globalId (the regex didn't work for auto-detecting short globalIds,  like `jacks3m`. A work around is to use your `it-{globalId}` account)
   - **Expiration Date** set `Permanent` to in most situations
   -  **Reason** should explain its reason for existing, e.g., "Sitefinty website project to allow access to old SharePoint", etc.
1. Verifying your new entry works
   - Now to test (while you wait for Networking to finish the ticket) you can add entry in your [hosts](C:\Windows\System32\Drivers\etc\hosts) file locally (e.g., `35.33.64.44 archive2.cmich.edu # comment: testing webdirector`)
   - In a new incognito browser session try to visit your new site (e.g., `archive2.cmich.edu/`) to test that you have set it up correctly

## References
- Code project for this WebDirect Admin app is call [RedirectManagement](https://code.cmich.edu/IT-AppDevelopment/CustomApplications/RedirectManagement)

## Tags
[[Redirect]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=RedirectTag)
[[Email]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=EmailTag)