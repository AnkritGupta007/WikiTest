

### AdminReg
* https://code.cmich.edu/IT-AppDevelopment/CustomApplications/AdminReg#permissions

### Apply admin dashboard AD groups (all need Amy Darnell's approval- especially Admins):
* staff: Apps-EssCMichApply-Staff
* staging: Apps-EssCMichApply-Uat
* admin:Apps-EssCMichApply-Admins

### DBCentral
* If the user is not already in the system, go to https://apps.cmich.edu/deafblindcentral/ and login with admin and password DbCentralAdmin!. 
* Once logged in, add a person for the new user.  
* Once the user is added, go to the DeafBlindCentral db on it-webdb and select the newly created user from the aspnet_Membership based on their email address. 
* With the UserId from this query, go and update their role in the [aspnet_UsersInRoles] table (2383166A-544B-4ABD-9235-7EC684B4370A is the RoleId for DBCentralAdmin, and 
C35A19AC-F478-4B43-B1AF-ECB815FDBCE5 is the RoleId for DBStaff)

### ECR AD groups:
* admins: OC-ECRAdmins
          https://miscel2.cel.cmich.edu/fc/asp/default.asp
* staff: OC-Group_ProfEd

### Financial Aid Portal
https://financialaidportal.apps.cmich.edu/home
* Admins (need approval from Kirk Yats) -- Add user to Apps-FinancialAidPortal-Admins AD group
* PowerUsers -- Add user to Apps-FinancialAidPortal-PwrUsers AD group

### (Old) Financial aid status page (or impersonate a student)
https://www.cmich.edu/centrallink/_layouts/FinancialAid/admin.aspx
* an admin needs to go to https://www.cmich.edu/centrallink/_layouts/FinancialAid/Permissions.aspx and add the user

### Global Campus intranet 
https://miscel2.cel.cmich.edu/intranet2a/

* roles="CENTRAL\OC-Group_ProfEd, CENTRAL\OC-Group_nonProfEd, CENTRAL\OC-Group_ProfEdStudents, CENTRAL\OC-BlueChipGroup"
* New employee needs access: Add to group their supervisor is in. 

For information about editing pages, see [How to Update Global Pages - Intranet](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-update-global-pages#info-for-intranet-staff-httpsmiscel2celcmicheduintranet2adefaultaspx)

### GoArmy
https://miscel2.cel.cmich.edu/GoArmy
* roles="CENTRAL\OC-Group_GoArmy"

### Prior Learning AD groups:
* evaluators: OC-PriorLearning-Evaluators
* coordinators: OC-PriorLearning-Coordinators
* admins: OC-PriorLearning-Admins
* advisors: OC-PriorLearning_Advisors (note the underscore instead of dash ... for some reason)

### SBT AD groups:
* admins: OC-SBT_Admins
* test-admins: OC-SBT-TestAdmins
* for center staff role user needs to return true from B_IS_CENTERSTAFF in `it-sql17-p-ocl.SBT` which comes down to having the user as an employee in `it-sql17-p-ocl.common.employee` and their pers_id from this table be the primary or alt contact in `it-sql17-p-ocl.common.responsible_center`

### TenNinetyEightT (1098T)
* Admins: Add to PortalAppConfig.dbo.Settings (WHERE [Application] = 'TenNinetyEightT' AND [Setting] = 'AdminUsers')

### Tuition Statement
* Admins: Add to TuitionStatementAdmins group in Active Directory (IT>Groups>Apps>TuitionStatement)
* Testers: Add to TuitionStatementTesters group in Active Directory (IT>Groups>Apps>TuitionStatement)


[[Accounts]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=AccountsTag)

