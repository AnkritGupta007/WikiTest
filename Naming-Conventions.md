# <a name="Top">Why use naming conventions</a>

Naming conventions are a set of rules for choosing the character sequence to be used for identifiers which denote variables, types and functions etc. in source code and documentation. 
 Reasons for using a naming convention (as opposed to allowing programmers to choose any character sequence) include the following:  
* to reduce the effort needed to read and understand source code.
* to enhance source code appearance (for example, by disallowing overly long names or unclear abbreviations).  

# Contents

1. [General](#General)  
1. [Repository and Project](#Repository)  
1. [HTML](#HTML)  
1. [JavaScript](#JavaScript)  
1. [SharePoint](#SharePoint)  
1. [C#](#CSharp)  
1. [SQL](#SQL)  

[//]: # (Start General)
# <a name="General">General Naming Conventions</a>
### Names
* **What** rather than **How**, don't expose the underlying implementation 
    * e.g. Use `GetNextStudent()` instead of `GetNextArrayElement()` 
* Long enough to be meaningful but short enough to avoid verbosity 
* Maintain compliance with the applicable language's rules and standards 

### Routines  
*   Avoid subjective names
    * e.g. `AnalyzeThis()`
*   Avoid class names in properties
    * e.g. `Book.Title` instead of `Book.BookTitle`  
*   Verb-noun method naming for routines
    * e.g. `CalculateInvoiceTotal()`
*   Overloads should perform a similar function

### Variables
* Append computation qualifiers (Avg, Sum, Min, Max, Index) to the end of a variable name where appropriate
  * e.g. `studentScoreAvg`  
* Use complementary pairs in variable names, such as min/max, begin/end, and open/close
  * e.g. `studentScoreMin` and `studentScoreMax`  
* Boolean variable names should contain prefixes that help the readability of the statement like Is, Has, etc. which imply Yes/No or True/False values
  * e.g. `fileWasFound`, `hasMACRAOAgreement`
* Avoid using terms such as Flag or Status​ when naming status variables, which differ from Boolean variables in that they may have more than two possible values, Instead of `documentFlag`, use a more descriptive name such as `documentFormatType`.
* Short-lived variable that may appear in only a few lines of code, still use a meaningful name. Use single-letter variable names, such as `i`, or `j`, for short-loop indexes only
* Do not use literal numbers or literal strings, such as `For i = 1 To 7`. Use named constants, such as `For i = 1 To NUM_DAYS_IN_WEEK`.
* Declare variables and initialize as a group at the beginning of a subroutine or function
* ​Avoid using the name **temp** when the variable is used for anything more than a swap variable or similar very short lived variable.  In other words, it should not be used except when you can see the instantiation from the line of code using the variable.

### Abbreviations
* Abbreviations should follow pascal casing. Single word abbreviations should have a capital first letter and multi word abbreviations should have a capital letter for each first letter  
  * e.g. `Id` for Identity, `CMich` for Central Michigan, `CMU` for Central Michigan University  

**[Back to top](#Top)**
 
[//]: # (End General)

[//]: # (Start Repositories and Projects)
# <a name="Repository">Repository and Project Naming Conventions</a>
We want to name repositories (repos) and projects with in repos with a similar style at CMU. This consistency helps you know how to search and what to expect in a given directory . For a step-by-step guide on how to do this click **[here](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-apply-naming-conventions-to-repositories-and-projects)**.

### What Naming to Use
```js
MyApp (Repo)
  /Model (Projects)
  /Persistence
  /Persistence.Tests
  /Web
  /Web.Integration.Tests
  /Web.Tests
  /Web.Ui
```

### What Naming ***NOT*** to Use

#### Bad Example 1
```js
CMich.MyApp (Repo) // No Prefix of "CMich"
  /CMich.MyApp.Model (Projects) // No Prefix of "CMich.MyApp"
  /CMich.MyApp.Persistence
  /CMich.MyApp.Persistence.Tests
  /CMich.MyApp.WebUi
  /CMich.MyApp.Web
  /CMich.MyApp.Web.Integration.Tests
  /CMich.MyApp.Web.Tests
  /CMich.MyApp // Often where "base" content was kept, but should now be put into proper buckets
```

#### Bad Example 2
```js
My-App (Repo) // No dash "-" between words
  /Ui (Projects) // Should be prefixed with Web or Mobile
```

**[Back to top](#Top)**

[//]: # (End Repositories and Projects)

[//]: # (Start HTML)
## <a name="HTML">HTML Naming Conventions</a>
### `id` Attributes
* The `id` attribute should only be used in special cases, such as to provide special jQuery behavioral functionality
* When used, `id` attributes should be in camel case format
```html
   <div id="superSpecialBehaviorThing"></div>
```
### `class` Attributes
* The `class` attribute should be used throughout the document for styling purposes. Main purpose classes should be in camel case format  
```html
   <div class="parentContainer"></div>  
```
* Modifications to existing classes should include the previous class name in lower case, a hyphen, and the name of the modification  
```html
  <div class="containerParent containerParent-maroon"></div>
```
### Elements
​The following should be used to organize page elements semantically:
* ​nav
* footer
* header
* section

This is not an exhaustive list. All HTML 5 elements can be found here: **[www.w3schools.com](http://www.w3schools.com/html/html5_new_elements.asp)**

[[HTML]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=HTMLTag)

**[Back to top](#Top)**  

[//]: # (End HTML)

[//]: # (Start JavaScript)
# <a name="JavaScript">JavaScript Naming Conventions​</a>
* Method names, variable names, etc. are camelCased.  One exception is when JSON objects original from a serialized C# object and the PascalCased names are part of the serialized object  
* Use jQuery as often as is practical when performing DOM manipulation to provide clean, common access to objects

[[Javascript]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=JavascriptTag)
  
**[Back to top](#Top)**

[//]: # (End JavaScript)

[//]: # (Start SharePoint)
# <a name="SharePoint">SharePoint Naming Conventions</a>
### Non Web Part/User Control Only Projects
These are projects that contain web parts and/or user controls along with other resources the web part or user control may depend on.

### Solution
Solutions should be named `CMich.SP.<ApplicationName>`. The application name should be Pascal naming convention and should not contain spaces nor special characters. Numbers are acceptable, if the number is not the first character in the application name.

Example: Project Personnel Transactions would be `CMich.PersonnelTransactions`

### Project  
Projects should be named `CMich.SP.<ApplicationName>`. The application name should be Pascal naming convention and should not contain spaces nor special characters. Numbers are acceptable, if the number is not the first character in the application name.
Example: Project Tuition Waiver would be `CMich.SP.TuitionWaiver`

### Namespace/Assembly Name
Namespaces/Assembly names should be `CMich.SharePoint.<ApplicationName>`. The application name should be Pascal naming convention and should contain no spaces or special characters. Numbers are acceptable, if the number is not the first character in the application name.
Example: Project Tuition Waiver would be `CMich.SharePoint.TuitionWaiver`

### Features/Packages
Features/Packages should follow the exact same name as the visual studio project (Project above).


### Web Part/User Control Only Projects
Projects that contain only generic (reusable) web parts or user controls (user controls and web parts should be in different projects).
There are already two solutions created for these two projects. `CMich.SP.WebParts` and `CMich.SP.Controls`.


#### Web Part Project Naming
Projects should be named `CMich.SP.WP.<WebPartProjectName>`. The web part project name should be Pascal naming convention and should contain no spaces or special characters. Numbers are acceptable, if the number is not the first character in the web part project name.
Example: Web Part Project Security Options would be `CMich.SP.WP.SecurityOptions`  

#### Name Space/Assembly Name
Namespaces/Assembly names should be `CMich.SharePoint.WebParts.<WebPartProjectName>`. The web part project name should be Pascal naming convention and should contain no spaces or special characters. Numbers are acceptable, if the number is not the first character in the web part project name.

#### Features/Packages
Features/Packages should follow the exact same name as the visual studio project (Project above)

[[SharePoint]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SharePointTag)  

**[Back to top](#Top)**

[//]: # (End SharePoint)

[//]: # (Start C#)
# <a name="CSharp">C# Naming Conventions</a>
### Routines
* Dispose of all objects that inherit from IDisposable

### Variables  
* Caps and Underscores for constants
    * e.g. `SETTING_KEY__INTRODUCTION_MESSAGE`  
* Pascal casing for methods/routines/properties
    * e.g. `CalculateInvoiceTotal`  
* Camel casing for variable names
    * e.g. `documentFormatType`
* Camel with an underscored (_) prefix for private class level variables
    * e.g. `_documentFormatType`
* Properties of a Private Class variable receive the same name without the underscore and pascal case rather than camel​
```c#
private bool _isStudent;

public bool IsStudent
{
         get { return _isStudent; }
         set { _isStudent = value; }
}
```  
* Declare variables and initialize as a group at the beginning of a subroutine or function. Use of Automatic properties is OK when the public property is merely wrapping a private class variable without any logic
* public string `FirstName { get; set; }`

[[C#]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSharpTag)  

**[Back to top](#Top)** 

[//]: # (End C#)

[//]: # (Start SQL)
# <a name="SQL">SQL Naming Conventions</a>
* Table names should be pluralized
  * e.g. `Classes` rather than `Class`  
* Identity columns should be named `<ENTITY_NAME>Id`
  * e.g. `ClassId` for table Classes  
* ​All SQL methods/conditions/etc... should be in UPPER case​  
  * e.g. `SELECT * FROM Table WHERE Column = 'value'`
* ​​​Names for attributes storing date or date/time related values should indicate in the name what is significant (i.e. if only date matters it should end in Date, if both are relevant then DateTime as a suffix is appropriate).  
  * e.g. `LastUpdatedDateTime` rather than `LastUpdated, BirthDate`
* ​​Boolean (bit) fields should still adhere to the General naming guidelines for boolean values  
* Don't duplicate the entity/table name in the attributes/columns EXCEPT for the identity column name listed above
  * Exception: Foreign keys may benefit by including the table name, but only do so if it increases readability.
* SQL column, table, stored procedure names, etc. should use PascalCasedNames
* Do not prefix SQL entities or procedures with names like `tbl`, `sp_`, etc.​​
  * Exception: In some cases adding the `v` prefix is helpful when working with views. Since tables and views are queried in an identical manner, including the prefix reduces confusion.

[[SQL]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SQLTag)  

**[Back to top](#Top)**  

[//]: # (End SQL)

### Tags
[[Conventions]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ConventionsTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[Development]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DevelopmentTag)

**[Back to top](#Top)**

