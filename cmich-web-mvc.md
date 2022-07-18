## ​Project Information  

*   ​.NET Version: 4.5.2 - 4.8
*   MVC Version 5.2.3.0  

*   CoreAPI References
    *   CMich
    *   CMich.ConnectionSettings
    *   CMich.Data
    *   CMich.Sap
    *   CMich.Web
    *   CMich.WebServices
*   Nuget Packages

*   ​ Microsoft.AspNet.Mvc - 5.2.3
*   Microsoft.AspNet.Razor - 3.2.3
*   Microsoft.AspNet.WebPages - 3.2.3
*   Microsoft.Web.Infrastructure - 1.0.0.0​

## ​Action Filt​ers  
### ​Layout Injector
#### Description  

​Allows changing of the master view for an action or controller with an attribute. This is extremely useful for applications that have multiple master views based on what user is currently logged in. A good example of this would be where an administrator has different navigation than a user. You could swap out the entire master view and still keep action views the same.  

#### Usage​

```c#
[CMich.Web.Mvc.ActionFilters.LayoutInjector("_layout2")]
public ActionResult About()
{
	return View();
}
```

### ​​​Sap Role Check  

#### ​​Description  

​Allows for checking if a user has a specific SAP role​ for a specific action or controller.  

#### ​Usage​

```c#
//Action Example
[CMich.Web.Mvc.ActionFilters.SapRoleCheck("WebDeveloper", MvcApplication.ApplicationMode)]
public ActionResult About()
{
	return View();
}

//Controller Example
[CMich.Web.Mvc.ActionFilters.SapRoleCheck("WebDeveloper", MvcApplication.ApplicationMode)]
public class HomeController : CMich.Web.Mvc.BaseController
{

}
```

## ​Attributes  
### ​Email  
#### ​Description   

​Validates email addresses. Since this was written this functionality is now built into the default MVC Attributes, this has been marked for deprecation. You can now use the DataType from DataAnnotations [https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx​](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatype.aspx)  

#### ​Usage  

There is no code example.  

### Max Word​​
#### ​Description  

​Allows for setting max word count for validation. This is an inclusive check, meaning if you enter 50 as the check a result with 50 words will be accepted.   

#### Usage

```c#
[CMich.Web.Mvc.Attributes.MaxWords(50, ErrorMessage = "{0} requires a maximum of 50 words")]
public string Description { get; set; }
``` 

### ​​​​​​​Month Day Year Required  
#### ​​​​​Description  

​Validates the ViewModel type CMich.Web.Mvc.Models.MonthDayYear. There is also an Editor Template build for this ViewModel type. It is recommended that you use all three of these together.  

#### ​​Usage

```c#
[CMich.Web.Mvc.Attributes.MonthDayYearRequired(ErrorMessage = "Month day and year are all required")]
public CMich.Web.Mvc.Models.MonthDayYear BirthDate{ get; set; }
```

### ​​​​​​​Month Year Required  
#### ​​​​​Description  

​Validates the ViewModel type CMich.Web.Mvc.Models.MonthYear. There is also an Editor Template build for this ViewModel type. It is recommended that you use all three of these together.  

#### ​​Usage
```c#
[CMich.Web.Mvc.Attributes.MonthYearRequired(ErrorMessage = "Error message you must select the month and year of your event")]
public CMich.Web.Mvc.Models.MonthYear MonthYear { get; set; }
```

### ​​​Must Be True  
#### ​​Description  

​Used to validate that a Boolean is true. An example use case for this would be, ensuring a user agreed to terms and conditions.  

#### Usage​​​​
```c#
[CMich.Web.Mvc.Attributes.MustBeTrue(ErrorMessage = "You must agree to the terms.")]
public bool AgreedToTerms { get; set; }
```
## ​​​​Base Objects  
### ​​​BaseController  
#### ​Description  

​This is a low level controller that all MVC controllers should inherit from directly or indirectly. Used in combination with the other base objects will populate properties for any ViewModel that implements IViewModel.  Your application MUST inherit from the base object HttpApplication in order to use this base object.   

#### Properties Available  

​ApplicationMode - Will contain the ApplicationMode supplied by the base object HttpApplication  

CurrentCMichUser - Will be populated with the current logged in or impersonated user supplied by the base object HttpApplication​. If the user is anonymous this property will be null

IsUserAuthenticated - When a user is anonymous this will return false otherwise true.

#### ​​​Usage

```c#
public class HomeController : CMich.Web.Mvc.BaseController
{
}
```

### ​​​BaseHttpApplication  
#### ​Description​  

​This is a low level HttpApplication that all MVC HttpApplications should inherit from directly or indirectly. By default this will take in the query string property CMichSwitchUserId and store it in the session for later use. This will allow for code to switch the current logged in user for testing purposes.   

#### ​Usage

```c#
public class MvcApplication : CMich.Web.Mvc.BaseHttpApplication
{
}
```  

### ​​BaseViewModel  
#### ​Description  

​This is a base ViewModel that implements the IViewModel interface. This ViewModel has the properties CMichUser and ApplicationMode, which will be populated automatically if you are inheriting from the BaseController object.  

#### ​Usage  

```c#
public class ExampleViewModel : CMich.Web.Mvc.BaseViewModel
{
}
```

### ​​​Controller  

#### ​Description  

​This is a high level controller that contains the CMichSession object. It is not recommended that you use this controller unless your project has already implemented it.   

#### Usage

```c#
public class HomeController : CMich.Web.Mvc.Controller
{
}
```  

### ​​HttpApplication  

#### ​​Description  

​This is a high level HttpApplication implementation. This assumes that you have the app setting "ApplicationMode" defined in your web.config. This HttpApplication will automatically switch the logged in user and is recommended that all basic applications use this inherit from this. This HttpApplication will give you ApplicationMode as a static property and CurrentCMichUser as a instance level property. CurrentCMichUser should be used instead of pulling the user's identity to get the GlobalId.  

#### Usage​​
```c#
public class MvcApplication : CMich.Web.Mvc.HttpApplication
{
}
```

## Tags
[[CoreApi]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CoreApiTag)
[[C#]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSharpTag)
[[MVC]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=MVCTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)


​