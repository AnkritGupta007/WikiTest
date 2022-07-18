## Database Information
As of December 2021, the primary database is `[PROD-COVID-Tracking]` on the `IT-WebDb` server.
We Priorities the ticket as `3` for Impact and `2` for Urgency.

## Approved Requestors
It is ok to provide information and complete requests by anyone in the 'Approved Requestors' section. If a user is not on this list please confirm with Nathan Fortier to either get them added to this list or deny the request.

### Covid Tracking
- Benjamin Coffman
- Busakorn "Piao" Satipanya
- Maxwell Heeke
### Faculty Personnel Services
- Ann Alvesteffer
- Kristen Skiver
### Human Resources
- Lori Hella 
### Student Affairs
- Shaun Holtgreive 
- Angella Coldwell
### Student Conduct
- Joe Finney
- Tom Idema
- Tricia Case

## Access to Shared Mailbox(s)
We do not have access to add to these directly however if we get a request we can point the helpdesk at these ad groups.
- LOB-UHS-covidtracking
- LOB-UHS-covidconnect
- LOB-UHS-covidtracing
- LOB-UHS-covidAssessment
- LOB-UHS-covidvaccine
- LOB-UHS-covidtestresults

## Access to Console Search Tool
[This is where the search tool is hosted for download](https://centralmichigan-my.sharepoint.com/:u:/r/personal/whitm1ek_cmich_edu/Documents/COVID/searchApp/win-x64/v2.0/CovidSearchConsole.exe?csf=1&web=1&e=U3qkJt&isSPOFile=1). No one will have access to this and Nathan Fortier or Eric Whitmore will need to add them to the shared list however in most cases Ben should be providing a computer with the software installed.

## Request to Verify a User's Data
The helpdesk can usually do this if the request is coming from the end-user directly. Sometimes the `Approved Requestors` will ask us to confirm if a user is vaccinated.

The simplest way to do this is to run the Stored Procedure [dbo.CheckStudentCompliance](https://cmich.teamdynamix.com/TDClient/664/Portal/KB/ArticleDet?ID=36628). The Stored Procedure will give data on the following (if available):
- Vaccination
- Uploaded Testing results
- Whether the user has been approved for an exemption
- Some basic info on the user, including their vaccination status

Sometimes we need to confirm if a user "attempted" to submit a vaccine card or test. This usually occurs when a user gets a confirmation email but the data doesn't seem to reflect that we actually received anything. Simply navigate to the shared folder `\\it-app-cab\healthscreen` and look for any submissions with their globalId. If the image is good (contains all the information we need) we can manually correct these.

## Request to Exempt a User (or list of users)
These might also be worded "remove this name from the Covid non-compliance list" which means "add to exemptions list".
### Background
Within the ticket(s), there should be info stating the student's global ID. If from Angella Coldwell it will also say whether the exemption request was approved or denied, but if from Tricia Case then know she only asks for those already approved. For these requests, you'll need to insert the data into the `[TestingExemptions]` table. If the request comes from Angella Coldwell we need to check if there are [pending exemptions](#pending-exemptions) for the user already.

### Info on Data to Insert
The [TestingExemptions] table has 5 columns of data we need to handle: `CreationDate`, `GlobalId`, `Type`, `Active`, `Notes`, and `Approved`.

- The `CreationDate` column will be the date of when you will insert data into the table, in the `YYYY-MM-DD` format
- The `GlobalId` column is the student's global ID will go
- The `Type` column will be set to 'OnlineStudent' or 'RemoteEmployee' 
- If the request is approved, the `Active` and `Approved` columns should be set to 1
- If the request is denied, the `Active` and `Approved` columns should be set to 0
- For either case of approved or denied requests, the `Notes` column bsaically acts as our documentation so it should mention:
  - The ticket number that we inserted/updated the record
  - Whether the request was Approved or Denied by the requestor

### Pending Exemptions

| Status | Active | Approved | Notes|
| --- | --- | --- | --- |
| Pending | `1` | `NULL` | Decision yet to be made. As long as **Approved** is NULL Angella Coldwell will get it in her AllPendingStudentExemptions report to process, regardless of the value of **Active**  |
| Approved | `1` | `1` | The most recent decision takes precedent |
| Denied | `0` | `0` | Was evaluated as not allowed an exception. Kept for historic record |
| Past Approval | `0` | `1` | Should never be in this state, but might in Spring 2022, or just delete the past semesters rows |
| Denied but bad update | `1` | `0` | Should never be in this state, but likely means a dev goofed up and didn't set **Active** to `0` properly |

1. After the status is **Approved** or **Denied** we need to add a row to `[TestingExemptions]` to reflect that
1. We also need to do clean up, deleting all **Pending** rows (i.e., **Approved = `NULL`) for that student

For more background info:
```SQL
-- This is the report that we send Angella every morning
-- This is under the Views section
SELECT *
  FROM [PROD-COVID-Tracking].[dbo].[AllPendingStudentExemptions]

-- And this is the raw exemption data, showing all users that may have a pending exemption
SELECT *
  FROM [PROD-COVID-Tracking].[CENTRAL\whitm1ek].[TestingExemptions]
  WHERE Approved is NULL
```

### Ways to Insert Data
The two main ways to insert data is by writing the INSERT query for the `[TestingExemptions]` table, or by right clicking the `[TestingExemptions]` table and selecting the "Edit X rows" option. This section is more about providing some suggestions to reduce the manual labor as there many be a decent amount of users to update/insert at one time.

Using the info from the section above, an example valid INSERT query could be:
```SQL
INSERT INTO [PROD-COVID-Tracking].[CENTRAL\whitm1ek].[TestingExemptions]
-- CreationDate, Student Global ID, Type, Active, Notes, Approved
VALUES ('2021-12-06', 'stude1nt', 'OnlineStudent', 1, 'Approved by Tricia Case - Ticket 1111111', 1)
```
// TODO: Describe VS code method of creating SQL query

### Request to Change a User's Data
This may be requested as "Resetting a persons COVID test status" or "Change positive test to a negative test status". The testing information is the **only** thing that we as a team should be changing at this point.
> ⚠ Nate Fortier or Eric Johnson deals with deleting any records, or asks for a [manual image upload](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/-/wikis/how-to-handle-covid-tdx-requests#how-to-manually-upload-a-new-image) if asked from the approved requestors above. 

> ℹ If a student or staff puts in a negative result that shouldn't have been entered, such as they didn't include the correct image. In this case we tell them to re-submit a new test result and image in the app, as we don't change this.

1. We look to find the record for the student and on the date mentioned on the ticket. 
   ```SQL
   SELECT *
     FROM [PROD-COVID-Tracking].[CENTRAL\whitm1ek].[TestingDetails]
     WHERE globalid = 'stude1nt' -- swap in the students GlobalId here
   ```
1. Look at the image in \\it-app-cab\healthscreen\covidtest\stude1nt-covidtest-20211125T102018.pdf and confirm that it is NEGATIVE
1. If it is negative in the image edit the value to `Negative` in the `TestType` column (In Edit mode or in a SQL UPDATE statement WITH A **WHERE** CLAUSE, but be Very careful to include the where clause)

## Request for Daily Healthscreen Data
This may be requested via a Service Request. Below are the steps per type of report requested:

### Specific Person Report

1. We look to find the record(s) for the person and on the date(s) mentioned in the ticket. 
   ```SQL
   SELECT *
     FROM [PROD-COVID-Tracking].[dbo].[CovidTrackingDetails]
     WHERE GlobalId = 'stude1nt' -- swap in the person's Global ID here
     AND CreationDate BETWEEN 'YYYY-MM-DD' AND GETDATE() -- swap dates as necessary
     ORDER BY CreationDate Desc
   ```
1. If using Microsoft SQL Server Management Studio, click the Results tab in the lower-half. Then, go to File > Save Results As... > Save as type (.csv). Name it something meaningful, such as `healthscreen-report-for-globalid.csv`. 

1. Then, open it in Microsoft Excel. You should format the `CreationDate` column to a meaningful format by selecting that column and right-clicking > Format Cells... > Date > `3/14/12 1:30 PM`. 

1. Next, save as an (.xlsx) file type since end-users are less familiar with the (.csv) type.

### Date Range Report

1. We look to find the record(s) for the date(s) mentioned in the ticket. 
   ```SQL
   SELECT *
     FROM [PROD-COVID-Tracking].[dbo].[CovidTrackingDetails]
     WHERE CreationDate BETWEEN 'YYYY-MM-DD' AND GETDATE() -- swap dates as necessary
     ORDER BY CreationDate Desc, GlobalId
   ```
1. If using SQL Management Studio, click the Results tab in the lower-half. Then, go to File > Save Results As... > Save as type (.csv). Name it something meaningful, such as `healthscreen-report-YYYY-MM-DD-thru-YYYY-MM-DD.csv`. 

1. Then, open it in Microsoft Excel. You should format the `CreationDate` column to a meaningful format by selecting that column and right-clicking > Format Cells... > Date > `3/14/12 1:30 PM`. 

1. Next, save as an (.xlsx) file type since end-users are less familiar with the (.csv) type.

## How to Manually Upload a New Image
Currently Nate Fortier, Eric Johnson and Eric Whitmore can manually place images in `\\it-app-cab\healthscreen\covidtest\`. 

Example ticket [4108592](https://cmich.teamdynamix.com/TDNext/Apps/393/Tickets/TicketDet.aspx?TicketID=4108592)

1. Download the image
1. Rename it {stude1nt}-vaccination-manualUpload.{png/jpg}
1. Add the file to \\it-app-cab\healthscreen\vaccination\
1. In Edit mode on `[PROD-COVID-Tracking].[CENTRAL\whitm1ek].[VaccinationDetails]` enter the needed fields


|Id	|CreationDate	|Globalid	|VaccinationDate	|VaccinationLocation	|VaccinationProofPath	|VaccinationType|
|---|---|---|---|---|---|---|
| {system generated} |{yyyy-mm-dd} | {studentGlobalId} |{read date from image}	|{read place from image}	| `\\it-app-cab\healthscreen\vaccination\{studentGlobalId}-vaccination-manualUpload.{png/jpg}` | {Moderna/Pfiser-BioNTech/Johnson & Johnson-Janssen}|

## Get a list of user's Vaccination Dates
Occasionally we get asked to check a list of users for vaccination records. All of these request's need to be approved by Shaun Holtgreive.

```SQL 
--GET LIST OF USERS AND VACCINATION DATES
SELECT GID
    , (SELECT MAX([VaccinationDate]) AS MaxVaccinationDate
    FROM            [PROD-COVID-Tracking].[CENTRAL\whitm1ek].[VaccinationDetails]
    WHERE        GlobalId = adb.gid) as Vaccination
FROM [ADBFeed].[dbo].[UserDataForWeb] adb
WHERE GID in ('stude1nt','stude2nt')
```