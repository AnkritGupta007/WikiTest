# Summary
All production deployments must follow the [CMU Change Management Policy](https://team.cmich.edu/oit/services/ServiceRelated%20Documents/OIT%20Change%20Management_ACTIVE.pdf).  The change management policy states that a change is defined as any modification to CMU production systems, planned or unplanned. In order to ensure the stability and reliability of OIT systems and services, OIT will manage changes through the three-stage process:

1. Requesting the Change
1. Approval of the Change
1. Implementation of the Change

# Deploying to Testing and Staging
For how to deploy to testing(betaweb) and staging(stgweb), click [here.](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-deploy-to-sharepoint)

# Requesting the Change/Deployment

## Creating the Change Ticket
1. Go to the ticket that requested the change for Sharepoint
2. Click Actions Dropdown
    * Create Parent
    * Change Calendar Item
3. Editing the Change Calendar Item
    * Set Requestor to yourself.
    * Set Ticket name to "Sharepoint Deployment - (Name of Project that was modified)
      * Ex. `Sharepoint Deployment - CMich.SP.EhsSISheet`
    * Add description of what change was requested and what changes were made to the Sharepoint site
    * Set Impact, Risk, and Type of Change according to [Change Management Process](https://cmich.teamdynamix.com/TDClient/KB/ArticleDet?ID=35842)
    * Set Team Performing Change to
      * App Dev (Whitmore)
    * Set Will this require a production outage?
      * Typically will be Yes, requires outage longer than a reset
        * Set Estimated Downtime to 15 minutes
     * Set Is communcation to campus or user offices required?
       * Typically No, but evaluate for the situation.
4. Once the Change Calendar Item is created, there should be a couple workflow steps to complete and updating the ticket feed.
   1. Update Changelog
       * Update the changelog with the changed made to the project or create a changelog and update it 
   2. Document Testing Steps
       * Describe how to test the changes so whoever deploys the change can verify that the updates were successfully implemented. 
   3. Update the ticket feed
      1. Click Actions (Dropdown)
      2. Click Update
      3. Click Templates -> Applications_Development -> Sharepoint Application Release
           * Filling this form out is straight forward, however try to keep it as simple as possible.
   4. Notify Matt Bailey for review of the ticket.
## Approval of the Change

### Approval Deadlines
- For Change Review Board (CRB) approved releases (based on *impact* and *risk*), the deadline is 4:00pm Monday
- For Director approved releases (based on *impact* and *risk*), the deadline is 12:00pm Wednesday

Throughout the week the Associate Director of Application Development will review tickets with a **Deployment Status** of *Requested* and post them to the [Change Calendar](https://team.cmich.edu/oit/services/Lists/Change%20Calendar/calendar.aspx).  Upon posting them to the [Change Calendar](https://team.cmich.edu/oit/services/Lists/Change%20Calendar/calendar.aspx), the **Deployment Status** will be changed to *Posted*.  The person doing the deployment will then wait for notification from the Change calendar on if and when they are able to proceed with the change.

## Implementation of the Change
After the change has been implemented the person doing the deployment will update the **Deployment Status** on the ticket to *Successful* or *Not Successful* depending on the outcome of the deployment.

## Tags
[[TeamDynamix]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TeamDynamixTag)
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[Deployment]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DeploymentTag)