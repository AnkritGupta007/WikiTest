[[_TOC_]]

# How to Update Global Pages
This page is intended to provided a starting place for remediating a variety of Global Campus tickets assigned to IT_APPLICATION_DEVELOPMENT in [TeamDynamix](https://cmich.teamdynamix.com/TDNext/Home/Desktop/Default.aspx).


## Info for Staff CRUD (e.g., bottom of the page on https://www.cmich.edu/global/cmuonline/Pages/programs.aspx) 

* Code: https://code.cmich.edu/IT-AppDevelopment/CustomApplications/PublicWeb
* Database server: `it-sql17-p-ocl`
* Database: `common`
* Tables:
  - `dbo.contact` - This contains contacts for all locations.  
    - The **center_code** column is used to represent location.  
    - The **contact_type** field is linked with `dbo.contact_type` and gives the title to display on the web.
    - The **contact_id** field links to `dbo.contact_info` table for the name.
  - `dbo.contact_info` - This table contains the employee information for a specific contact.  New employees need to be added here (If there is a need for a placeholder, one exists with a contact_id of 1425.).
  - `dbo.contact_type` - This table represents the contact's position information.  New contact types might need to be added to accommodate the "web" titles of the contacts, which is not always the same as you would find in SAP.
* Picture: 
  - Crop and resize the picture to 110x110 (not sure if this is the correct size, but some of the previous images were of this size). 
  - Rename it to the contact_id (e.g., 1234.jpg) 
  - Go to https://www.cmich.edu/global and choose the s Site Contents in the SharePoint wheel in the top left. 
  - Then go to Images -> People. Upload the picture there. Once uploaded press on the "..." symbol on the bottom right side of the picture you uploaded. 
  - Click on "..." and then Check In. Choose the major version and click OK. 

## Info for Intranet Staff (https://miscel2.cel.cmich.edu/intranet2a/default.aspx) 
For information about granting access, see [How to Grant Access](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-grant-access#global-campus-intranet).

* Code: https://code.cmich.edu/IT-AppDevelopment/global-legacy/vss-2005-transfer 
* Database server: `it-sql17-p-ocl`
* Database: `common`
* Tables:
  - `dbo.employee` - contains employee information that appears on the /directories/employee-detail.aspx page.

## Degrees & Programs
The pages for viewing degrees in Global Campus are put together from several data sources, which can make modifying them or creating new ones a rather difficult task. The javascript is pulled from the CDN at `\\it-prdcdn01\cdn\global\web\js\gc-programDetail.min.js`; this minified file is built as part of the [PublicWeb](https://code.cmich.edu/IT-AppDevelopment/CustomApplications/PublicWeb) project, specifically [gc-programDetail.js](https://code.cmich.edu/IT-AppDevelopment/CustomApplications/PublicWeb/-/blob/master/PublicWebJS/App/gc-programDetail.js). Most of this documentation is written by reverse-engineering that file and the various controllers and other JavaScript it calls into; anything not covered by this page can likely be worked out from that code or from editing the degree detail page in SharePoint to get the HTML referencing it. (The HTML *ought* to be present in a file in the PublicWeb API as well, but it's unmaintained and therefore not useful.)

### Sources
Degree pages for Global Campus pull from several sources (many of them non-obvious due to the way they're loaded through the API), but in general, they can be grouped into two main sources:
1. The `it-sql17-p-ocl` database server (testing/staging sites use `it-sql17-t-db1`), the `common` and `mis` databases in particular
2. Sharepoint

Adding a new degree or updating one will require a fairly detailed list of what is changing and where; many fields lack documentation, so often the only way to be *certain* of what should be provided is to copy the field from a previous version of the degree (or one of the same levels for a new one).

#### `it-sql17-p-ocl`
There are several tables in the `it-sql17-p-ocl` database that need to be updated to affect the content displayed on the page. The *most important* tables are:

##### mis.dbo.degrees2
This table lists degrees with their descriptions, as well as the CM_SC_ID and CM_CG_ID used by CRM. New records require many fields best determined by using an existing and similar record as an example; updates to existing degrees require the following updates:
- `DegreeDescription`: Set this to the new title to display as the header for the page.
  - Example: 'Bachelor of Science, Major in Organizational Leadership'
- `MajorDescription`: Set this to the name of the concentration to display.
  - Example: 'Organizational Leadership'
- `description`: This is a fallback description not generally used on the webpage itself, but should be updated to ensure names in it are correct if one already exists.
- `DegreeCode`: This is the code used for matching to degrees in other tables, and in the URL to specify which degree to display.
- `MajorCode`: Known as the "concentration code" elsewhere, this is the code used to specify a specific major within a program, or a specific concentration within a major depending on how the degree is configured. This is the other part of the code in the URL for a page, and can be used to have multiple concentrations for the same page.
  - Example: 'BS-OL'
- `CM_SC_ID`: The ID of the program in SAP; this should also match the related record in `common.dbo.SCPrograms`. This value is also sent to CRM for things like requests for information.
- `CM_CG_ID`: The ID of the module group in SAP; this should also match the related record in `common.dbo.CMProgSpecAreas`. This value is also sent to CRM for things like requests for information.

##### common.dbo.CMProgSpecAreas
This table lists entries related to Module Groups in SAP, and can be joined to `mis.dbo.degrees2` by `degrees2.CM_SC_ID = CMProgSpecAreas.ProgID AND degrees2.CM_CG_ID = CMProgSpecAreas.ModGrpID`. Entries here are fairly straightforward copies of what's in SAP; the only caveats here to watch out for are:
- `AcadYear` MUST be '2007 - 2008' for any new entries; the business logic related to the site isn't actually able to correctly handle differing academic years, so creating anything earlier won't display and creating anything later will cause all other degrees to stop being displayed.
- If a change involves a new ProgID or ModGrpId, it should be created as a new record instead of an update to the old record. This leaves the old record in place so that records referencing it can still find the old version they were made from.

##### common.dbo.SCPrograms
This table lists entries related to Programs in SAP, and can be joined to `mis.dbo.degrees2` by `degrees2.CM_SC_ID = SCPrograms.ProgID`. Entries here are fairly straightforward copies of what's in SAP; the only caveats here to watch out for are:
- `AcadYear` MUST be '2007 - 2008' for any new entries; otherwise, they won't match the version in CMProgSpecAreas and won't show up.
- `AcadLevel` is either 'DR', 'GR', or 'UG'. Depending on which, `LevelDescr` is either 'Doctoral', 'Graduate', or 'Undergraduate' respectively and `DegreeType` has one of a few values with more information (i.e. 'Bachelors Degree', 'Undergraduate Certificate', or 'Undergrad 2 Year Certificate' for UG programs).
- Campus is set to either 'CEL' (Online) or 'ONC' (On Campus).
This table is also where the credits displayed can be updated.

##### common.dbo.SharedContent
This table contains HTML for display on a given page, either by the degree code or major code (concentration code) in `mis.dbo.degrees2`, or the site code in `common.dbo.SITES` for sites. The main thing used is the `Html` column, which is used for the main description of the degree in the space below the banner image and such. The `CustomHtml` column is poorly named; it holds a JSON object specifying other parts of the page that can be replaced as needed. It's rarely used for degrees and concentrations, but can be used to add badges or to specify a replacement image from the one that would otherwise be used.

**NOTE**: Some shared content can be edited by using the [Content Manager](https://globalapp.cmich.edu/contentmanager/#/) ([Betaweb version](https://globalapp.cmich.edu/dev/contentmanager/#/))  

##### common.dbo.loc_degree
This table lists locations (sites) where a given degree is offered. Listings here are fairly straightforward, matching a site code to a degree and concentration with a status and the start and end terms (with '9999999' as the end term if there are no plans to end the degree offering). To rename a degree or concentration, take any records for the old degree code and concentration and set the `AppEndTerm` to the last term it will be offered under that name, and then add new entries copying them for the new degree/concentration code with the `AppStartTerm` set to the first term it's offered under the new name and an `AppEndTerm` of '9999999'.

Statuses work in particular ways, though. Some are outdated or deprecated, so the following is how to determine a status for a new degree.
- If the degree should be available online globally, there is a special 'CDL' site used for this purpose; simply create an entry to set the status for that site code to 'AVAIL'. If there are certain states that the degree must be filtered *out* of, add them to the comma-separated list in the `StatesNotAllowed` column of `mis.dbo.degrees2`.
- For other sites, there are four relevant statuses:
  - AVAIL: Shows a degree as available for face-to-face instruction at that location.
  - COMBO: Shows a degree as available for hybrid instruction at that location.
  - OL: Shows a degree as available for online-only instruction at that location.
  - SUSP: Suspends an offering for a degree at a given location without needing to erase the record here.
  - COHRT: Designates that a degree has cohort enrollment rather than open enrollment, even if it's not listed in one of the other cohort tables

##### cm_download.dbo.GetCohortInfoForSite
This is a stored procedure rather than a table, but used to get the base information on degrees with cohort enrollment for a given site. In theory, at least; in reality most degrees seem to be marked using the COHRT status alone, or the following table.

##### common.dbo.ApplyByOverride
This is more specifically about "Apply By Override" for cohorts, and an entry here is a third way to mark that a given degree is offered as a cohort rather than by open enrollment. These entries have to have specific dates, and if an entry's `StartDate` isn't in the future then it will be ignored.

##### common.dbo.SITES 
This table lists all the sites of global campus. To hide all online programs under Degrees and Programs at a particular site, `DisplayOnline` attribute of that site should be set to 0. It should be set to 1 to show all the online programs under Degrees and Programs.

#### Sharepoint
The rest of the display is taken from Sharepoint, primarily from the [SharedHtml](https://www.cmich.edu/global/Lists/SharedHtml/AllItems.aspx) list in the Global Campus site. (Here is the [testing version](https://betaarchive.cmich.edu/global/Lists/SharedHtml/AllItems.aspx) and [staging version](https://stgarchive.cmich.edu/global/Lists/SharedHtml/AllItems.aspx) of the SharedHtml page.) Images for the top banner are taken from the list at [Images > Degrees](https://www.cmich.edu/global/PublishingImages/Forms/Thumbnails.aspx?RootFolder=%2Fglobal%2FPublishingImages%2FDegrees). (Here is the [testing version](https://betaarchive.cmich.edu/global/PublishingImages/Forms/Thumbnails.aspx?RootFolder=%2Fglobal%2FPublishingImages%2FDegrees) and [staging version](https://stgarchive.cmich.edu/global/PublishingImages/Forms/Thumbnails.aspx?RootFolder=%2Fglobal%2FPublishingImages%2FDegrees) of the Images > Degrees page.) There are several types of HTML snippet that can be used here, with generally reasonable defaults if nothing is provided; a sample of those tested so far is below. New or changed items in the SharedHtml list have to be approved before they'll show up, but you can approve your own changes.

##### LevelRequirements
If this is provided for a degree program, it will override the default displayed at the top of the program requirements tab for the given degree level. If nothing is created here then the default for a graduate/undergraduate/doctoral-level degree will be used, based on the level of the degree in question.

##### OverrideRequirements
If this is provided for a degree and concentration, it will override the displayed list of courses for the concentration in question (in the Program Requirements tab) with the provided HTML. If nothing is provided here, the list will be created from the bulletin specifications in the `AcademicStructure` database (on the `it-sql17-p-ocl` server). This is *generally* what ought to be done, but sometimes it will need to be overridden if the bulletin hasn't been updated yet or if Global Campus wants something different displayed due to differing requirements or alternatives offered online.

> ℹ For Example: A ticket asks to have degree concentration MA-LDT Program Requirements altered so the long-name of EDU 632 includes "(6 hours)"
> - Filter the SharePoint List of [SharedHtml](https://www.cmich.edu/global/Lists/SharedHtml/AllItems.aspx) down to just the **Type** of "OverrideRequirements" 
> - Further filter the **Title** to only include "MA-LDT" 
> - If none exists, you would create it based on whats currently on the rendered HTML page
> - Now Click the `...` button and select **Edit Item**
> - In the **Format Text** tab, click **Edit Source** to alter the HTML to include "(6 hours)" after the EDU 632 link.
> - Click **OK** to preview the change
> - Click **Save** and then [Approve](https://www.cmich.edu/global/Lists/SharedHtml/mod-view.aspx) the change

##### DegreeAdmissionRequirements
If this is provided for a degree, it will override the generic admission requirements for the degree level displayed in the "Admission Requirements" tab. This may need to be overridden if Global Campus has a particular online application form for a degree or additional information they'd like to display here.

## Request For Information (Global Information Packets)
* Request for Information: https://www.cmich.edu/global/programs/Pages/degrees.aspx?dc=BS-ED&cc=ECD (dc = degree, cc = concentration)
* Document Download: https://www.cmich.edu/Global/Future/Pages/infoDownload.aspx?dc=BS-ED&cc=ECD (dc = degree, cc = concentration)
* Document Library: https://www.cmich.edu/global/InfoPacks/Forms/AllItems.aspx
* Database server: `it-sql17-p-ocl`
* Database: `mis`
* Tables: 
  - `mis.degrees2` - Degrees and Concentrations are linked to the InfoPack document by getting the info_path_link where the DegreeCode = dc and MajorCode = cc.  The info_path_link should point to the correct file in the SharePoint Document Library.

**Note**: Sometimes new entries will need to be added to _mis.degrees2_ table.  We need to add documentation for that here.

## Custom application start and apply by dates
* `it-sql17-p-ocl` `common.dbo.ApplyByOverride`

## Create Vanity/Shortened URLs for Global Lead Forms
Add the directory under the Global.cmich.edu site on `oc-vm-iis8` then set up HTTP redirect.

## Update Tuition and Fees page
* Database server: `it-sql17-p-ocl`
* Database: `common`
* Tables:
  - `dbo.internet_costs`

## How to remove/add a global campus when it is closed or reopened
   
A ticket like [Service Request #3882402](https://cmich.teamdynamix.com/TDNext/Apps/393/Tickets/TicketDet?TicketID=3882402) can be expected when a global campus is closed or open. 

The global campus center are populated on the website through PublicWeb Api which interacts with database server: `it-sql17-p-ocl` The API looks for each degree in `dbo.Degrees` in the `common` database, and then populates the global campuses for each degree by interacting with `dbo.loc_degree.` So, removing a specific global campus involves the following steps:

* Go to server `it-sql17-p-ocl` > db `common` > table `dbo.loc_degree` in , and search for all the degrees where the center is involved by its code. 
> ℹ Hint: Example SQL would be `SELECT TOP (1000) * FROM [common].[dbo].[loc_degree] WHERE [code] = 'TROY'`

* Change the status for all the rows involving that center to 
   - `SUSP` if the center is closed permanently
   - `CLOSE` if the center is closed temporarily
   - `AVAIL` if the center is reopened

** Note: The Admissions database may also need to be updated.  If so, see [Remove Center / Program / Major from the off campus programs section](https://code.cmich.edu/IT-AppDevelopment/CustomApplications/Admissions#remove-center-program-major-from-the-off-campus-programs-section-applicationenrollmentcenterandprogram) in the Admissions project README.

## Steps to remove/add global campus as a proctor designation

This documentation is created to assist adding or removing a global campus center as a proctor designation. One of the tickets requiring the above request was this [ticket- 3909081](https://cmich.teamdynamix.com/TDNext/Apps/393/Tickets/TicketDet.aspx?TicketID=3909081)

1. Global campus site uses the database `it-sql17-p-ocl`. So, go to `it-sql17-p-ocl`, and open the [common].[dbo].[SITES] table.
2. Search for the global center which is to be removed/add as proctor designation.
3. Set the column value of 'Proctor' to 1 if the center is to be added as a proctor designation, and set the value of 'Proctor' to 0 if the center is to removed. 
4. Make all the above changes in it-webDb database as well to maintain consistency.

## SQL for [EOC](https://code.cmich.edu/IT-AppDevelopment/CustomApplications/EOC) (`it-sql17-p-ocl`)

```sql
USE [EOC_ONLINE] 
 
DECLARE @SLCM_term_from AS char(7) ---int
DECLARE @SLCM_term_to  AS char(7) ---int
DECLARE @PE_term AS varchar(10)

SET @SLCM_term_from = '2020300' 
SET @SLCM_term_to = '2020300'
SET @PE_term = '%' --Variable used for LIKE comparison

SELECT SI.SLCM_term AS 'SCLM Term'
	,SI.ProfEd_term AS 'Global Campus Term'
	,CONVERT(varchar, SI.start_date, 101) AS 'Course Start Date'
	,CONVERT(varchar, SI.end_date, 101) AS 'Course End Date'
	,SI.designator AS 'Course'
	,SI.EPN 
	,II.last_name AS 'Instructor Last Name'
	,II.first_name AS 'Instructor First Name'
	,SI.instructor_global_id AS 'Instructor ID'
	,SI.site_name AS 'Center'
	,L.name AS 'Cost Center'
        ,NR.[value_mean] AS 'Q8 Mean'
        ,NR.[value_std_dev] AS 'Q8 Standard Deviation'
        ,NR.[value_count] AS 'Q8 Number of Responses'
        ,SC.cnt AS 'Q8 Number of Students in Course'
        ,1.000 * NR.[value_count] / SC.cnt AS 'Response Rate'
        ,[declined_count] AS 'Number of Students Declining to Respond to Survey'
        ,S.CourseType AS 'Course Type'
        ,CT.Name
  FROM [dbo].[VIEW_NONTEXT_RESPONSES_VALUE_SUMMARY_BY_SURVEY_INSTANCE] NR INNER JOIN dbo.VIEW_SOS_REPORT_RELATED_INFO SI
	ON SI.[survey_instance_id] = NR.survey_instance_id AND NR.instructor_id = SI.instructor_id INNER JOIN dbo.VIEW_SURVEY_INSTANCE_INSTRUCTOR_INFO II
	ON NR.instructor_id = II.instructor_id AND NR.survey_instance_id = II.survey_instance_id LEFT JOIN (SELECT survey_instance_id, count(*) AS cnt FROM dbo.VIEW__SURVEY_INSTANCE_TO_CONSTITUENT_ASSOCIATION GROUP BY survey_instance_id) SC
	ON SC.survey_instance_id = SI.survey_instance_id LEFT JOIN dbo.VIEW__MIS__FC_SCHEDULING S
	ON SI.EPN = S.crn LEFT JOIN [it-sql17-p-ocl].Common.dbo.LOCATIONS L
	ON S.LocationCode = L.code AND L.EOC = 1 INNER JOIN [EOC_ONLINE].[dbo].[VIEW_RESPONSE_COUNTS_BY_SURVEY_INSTANCE] RC
	ON RC.survey_instance_id = NR.survey_instance_id LEFT JOIN [it-sql17-p-ocl].mis.dbo.FC_CourseTypes CT
	ON CT.Code = S.CourseType
  WHERE NR.QUESTION_ID = 7 AND NR.survey_instance_id > 1
	AND SI.SLCM_term BETWEEN @SLCM_term_from AND @SLCM_term_to AND SI.ProfEd_term LIKE @PE_term
	AND SI.end_date >= '10/20/2019'

```

## Tags
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[Global]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=GlobalTag)