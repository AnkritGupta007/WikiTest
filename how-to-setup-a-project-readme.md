# Summary
The purpose of this how to is to provide step by step instructions on how to setup a readme page and to define what elements are required and which elements are optional on the readme page.

## Readme setup

* **Option 1** - create a empty file called README.md in the root of your project folder
* **Option 2** - Click the README link after you create a new project

   ![readme_gitlab](/uploads/5c8cfacefb704a60d90fe7e9744716f3/readme_gitlab.png)


## Required
---
* **Build Status and Coverage Badges** - Badges indicate a successful or failed build and testing coverage
* **Status** - New/In Production/Not In Production
* **Project Summary** - The purpose of the project. *Write a few sentences, to explain for developers new to the app, who the common users are and what they do in the application as an overview.*
* **Division(s)** - Which division(s) the project belongs to
* **Business Owner(s)** - Person(s) who can provide authorization for changes *and* their title (so if they move on we can look up the their replacement). For those project who don't currently have business owners please use "unknown"
* **Business Subject Matter Expert(s)** - Person(s) who can provide answers to most business process related questions *and* their title (so if they move on we can look up the their replacement). For those project who don't currently have business owners please use "unknown"
* **Technical Owner(s)** - Person(s) who have development expertise on this app
* **Web Server Info** - (Web Only) List the branches, paths, and URLs
* **Databases** - List the branches, database servers, and databases associated with the project
* **SAP Dependencies** - (If SAP is used) List SAP RFCs or tables used by this project
* **Deployment information** - List the production and test deployment information including unc paths, servers, etc.
* **Deployment Considerations** - When to deploy or when not to deploy.  List dependent systems, etc.
* **Impact of Outage** - (High/Medium/Low) - Description of impact.
* **Audience** - Students/Faculty/Staff/Public
* **Last ADA/508 Audit** - when was ADA last assessed for this project (if ever).

## Optional
---
* **Notes** - Should include common gotchas, how to resolve frequent ticket request, or modify permissions, etc.
*  **Logging Information** - Information on how to obtain error logs.
*  **Training** - How to obtain training.
*  **Other information** - Please include any other information which would be helpful on the project.

## Base Template
```md
# ProjectName

| Branch | Build Status | Coverage Status |
| ------ | ------------ | --------------- |
| **Master** | [![build status]({ProjectURL}/badges/master/build.svg)]({ProjectURL}/commits/master) | [![coverage report]({ProjectURL}/badges/master/coverage.svg)]({ProjectURL}/commits/master) |
| **Testing** | [![build status]({ProjectURL}/badges/testing/build.svg)]({ProjectURL}/commits/testing) | [![coverage report]({ProjectURL}/badges/testing/coverage.svg)]({ProjectURL}/commits/testing) |
| **Staging** | [![build status]({ProjectURL}/badges/staging/build.svg)]({ProjectURL}/commits/staging) | [![coverage report]({ProjectURL}/badges/staging/coverage.svg)]({ProjectURL}/commits/staging) |
| **Production** | [![build status]({ProjectURL}/badges/production/build.svg)]({ProjectURL}/commits/production) | [![coverage report]({ProjectURL}/badges/production/coverage.svg)]({ProjectURL}/commits/production) |

## Status
<!-- New / In Production / Not In Production -->

## Project Summary
<!-- The purpose of the project. Write a few sentences, to explain for developers new to the app, who the common users are and what they do in the application as an overview.-->

## Division / Department
<!-- Which division(s) or departement(s) does the project belong to -->

## Business Owner(s)
<!-- Person(s) who can provide authorization for changes and their title (so if they move on we can look up the their replacement). For those project who don't currently have business owners please use "unknown" -->

## Business Subject Matter Expert(s)
<!-- Person(s) who can provide answers to most business process related questions and their title (so if they move on we can look up the their replacement). For those project who don't currently have business owners please use "unknown" -->

## Technical Owner(s)
<!-- Person(s) who have development expertise on this app -->

## Web Server Info
<!-- List the branches, paths, and urls -->
| Environment | UNC Path | URL |
| ----------- | -------- | --- |
| **testing** | `UNCPATH` | [URL](URL) |
| **staging** | `UNCPATH` | [URL](URL) |
| **production** | `UNCPATH` | [URL](URL) |

## Databases
<!-- List the branches database servers and databases associated with the project -->
| Environment | Server | Database |
| ----------- | ------ | -------- |
| **testing** | server | database |
| **staging** | server | database |
| **production** | server | database |

## SAP Dependencies
<!-- List SAP RFCs or Tables used by this project (Remove if not needed) -->
### RFCs / Tables
| Type | Name |
| ---- | ---- |
| **RFCs** | CommaSeparatedListOfRfcs |
| **Table** | CommaSeparatedListOfTables |

## Deployment Considerations
<!-- When to deploy or when not to deploy.  List dependent systems, etc. -->

## Impact of Outage
<!-- `Critical` > 250 users/ `Major` 11 to 249 users/ `Minor` < 10 users -->
<!-- Description of impact. -->

## Audience
<!-- Select all that apply -->
- [x] Students
- [x] Faculty
- [x] Staff
- [ ] Public

## Last ADA/508 Audit
<!-- When was ADA last assessed for this project (if ever). -->

<!-- Optional -->
<!-- ## Notes -->
<!-- ### How To Run Locally -->

<!-- ### Logging Information -->
<!-- Information on how to obtain error logs. -->

<!-- ### Gotchas -->
<!-- Information for things that might trip up a new developer in the app. -->

<!-- ### How to resolve frequent ticket request -->
<!-- Information like how to add permissions or resolve frequent ticket request. -->

<!-- ### Other information  -->
<!-- Please include any other information which would be helpful on the project. -->
```


## Example
---
[ITSM Connect](https://code.cmich.edu/App-Middleware/ITSMConnect)

## Tags
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[ProjectManagement]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ProjectManagementTag)
