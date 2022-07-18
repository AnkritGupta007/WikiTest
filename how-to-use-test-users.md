# Summary
The following passwords and user accounts are handy when testing things like password changes or security question validation.  The do exist in AuthDB, local AD and Azure AD and each has an O365 mailbox. *They do* ***NOT*** *exist in SAP.* They can be used for authentication testing.

## Rule on test profiles: 
- **Always** reset the password back to the original at the end of each round of testing, so that the next person to use it knows the password

## Table of Test Profiles
| **Test User Global ID** | **Password `(Always restore back to original)`** | **Date of Birth** | **Last 4 of Soc** |   **Security Question**     |
| :---------------------- | :--------------------------------------: | :-----------: | :-----------: | :---------------------------: |
| stu1tt                  |               init5Xpass#3               |  05/05/1955   |     rt04      |      met spouse? *here*       |
| fac1tt                  |               init5Xpass#3               |  05/05/1955    |       rt01       |              Orange Cat ? *loki*           |


## Tags
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[Database]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DatabaseTag)
[[Office365]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OfficeThreeSixtyFiveTag)