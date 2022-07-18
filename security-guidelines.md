## Regulations

We must be aware that much of the data we work with is associated with student data protected by the Family Educational Rights and Privacy Act ([FERPA​](http://www.ed.gov/policy/gen/guid/fpco/ferpa)) and increasingly, due to our interactions with CMED, with student and patient data that is protected by Health Insurance Portability and Accountability Act ([HIPAA](http://www.hhs.gov/ocr/privacy/)).

We must be educated about what these regulations require in order to ensure we are attempting to comply with these directives.

HIPAA-protected data must reside on machines and environments that are HIPAA compliant, which impacts deployment scenarios.  FERPA provides direction on who may access what kind of student data and under what auspices this can be done.

We also have policies and guidelines in place at CMU to protect accounts by mandating we not ask users for passwords, etc.

## Guidance

### Databases

We strive to use SQL Server integrated authentication whenever possible to protect connection string credentials from being compromised due to inadvertent file sharing or other exposure.  This typically means that connections to databases depend on the application pool identity being configured in IIS as well as safe database permissions and use of the domain account permissions the site typically runs under.  Ideally the same domain account runs the application in our QA and Production environments to eliminate one potential source of deployment issues.  Clear text passwords must not be stored in any database.  If passwords must be stored for credential verification in scenarios (which should be very rare) where CMU Active Directory authentication is not possible they must be salted and hashed to add some additional security in case of a database compromise.

### HTTPS

HTTPS must be used to protect user credentials for resource access.  No credentials should be requested except for over HTTPS.  For applications that provide access to privileged data (i.e. that protected, in general, by FERPA and HIPAA regulations), SSL should be use for the entirety of the user's session. 

### Cookies

Cookies should not include, where possible, user-sensitive information beyond session identifiers.  These should be protected via SSL usage and should not be persisted on the browser.  In general, due to the kiosk nature of many of the lab environments on campus and the potential for users to not close browsers adequately, etc., developers should strongly consider not persisting any cookies beyond the session except where a user explicitly acknowledges he/she is using a personal, private device.

### ​Querystrings

Any information passed in query strings should be either a) non-identifiable (i.e. no harm in manipulating for use) or b) be validated with a validator that is a hash of the contents of the query string parameter values combined with a shared secret (and possibly a salt for additional entropy) so the executing server may validate the credentials by repeating the hashing process on the provided contents along with the same private secret (not passed in the query string) so the validator and result may be compared to identify query string corruption or manipulation.  Never use the query string for providing SQL statements to execute, role assignment (i.e. ?isAdmin=1) or other sensitive actions subject to user manipulation whereby they may gain additional privileges or access not available to them.

### User Roles

Depending on the scenario, roles can be handled in a multiplicity of ways. When the rights are to be more closely associated with the position a user holds vs. the user himself/herself, then the rights should typically be managed by using SAP roles.  We have MVC attributes that can assist with this.  When the user's credential (i.e. Global ID) is what is to retain the role, then using AD verification of user rights via group membership is an accepted practice.  Ensure that test sites remain closed to unauthorized individuals if they capture user data in order to prevent inadvertent submission of data meant for a production system to a test system (a la early apply.cmich.edu rollout).  Administrative interfaces should always be protected and should never be anonymously available.

## Policies

We must be transparent and forthright in sharing knowledge of any breach, or attackable applications with management in order to secure the issue and protect user data.  This is a legal issue that requires us to comply.  This is not flexible.  Management will provide guidance on the next immediate steps.

## Tags
[[Policies]](https://code.cmich.edu/search?group_id=&project_id=365&repository_ref=master&scope=wiki_blobs&search=taggedWithPolicies)
[[OldWiki]](https://code.cmich.edu/search?group_id=&project_id=365&repository_ref=master&scope=wiki_blobs&search=taggedWithOldWiki)
