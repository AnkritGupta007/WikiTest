# Summary
​​​​​​​​​This article describes how to setup an MVC application to use *Google's* "I'm not a Robot" captcha called **reCAPTCHA**.

# Starting Steps
Work has been done to add a C# class to **CMich.Web.Mvc.ReCaptcha** and other supporting code such as using a WebProxy in RES and STG . 

Be sure to use get the latest on https://code.cmich.edu/IT-AppDevelopment/Shared-Libraries/CMich.CoreApi.Web of CMich.Web and Cmich.Web.Mvc to have all the needed infrastructure that's been added before you begin.
​
# Steps (In no particular order)
## Modify You Web.config
​​You will need to add the `<add key="ProxyServer" value="False"/>​​` line to your Web.config

```xml
<!-- // EXAMPLE -->
<configuration>
    <appSettings>
        <add key="webpages:Version" value="3.0.0.0"/>
        <add key="webpages:Enabled" value="false"/>
        <add key="ClientValidationEnabled" value="true"/>
        <add key="UnobtrusiveJavaScriptEnabled" value="true"/>
        <add key="UnobtrusiveJavaScriptEnabled" value="true"/>
        <add key="ApplicationMode" value="Development"/>
        <add key="IsSapApplication" value="False"/>
        <add key="ProxyServer" value="False"/>​
    </appSettings>
...
</configuration>
```

​And <add key="ProxyServer" value="True" xdt:Transform="SetAttributes" xdt:Locator="Match(key)"/> in your Web.Testing.config and Web.Staging.config​

```xml
<!-- // EXAMPLE -->
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">​
    <appSettings>
        <add key="ApplicationMode" value="Testing" xdt:Transform="SetAttributes" xdt:Locator="Match(key)"/>
        <add key="ProxyServer" value="True" xdt:Transform="SetAttributes" xdt:Locator="Match(key)"/>
    </appSettings>
  <system.web>
    <compilation xdt:Transform="RemoveAttributes(debug)" />
  </system.web>
</configuration>
```

## Modify Your Global.asax

Here we need to enable use of a proxy server by adding the lines 

from `//start of add` 

to `//end of add`


```c#
// EXAMPLE
public class MvcApplication : CMich.Web.Mvc.HttpApplication
{
   //start of add
   private static bool _useProxyServer = false;
 
    public static bool UseProxyServer
    {
        get
        {
            return _useProxyServer;
        }
        set
        {
            _useProxyServer = value;
        }
    }
 
    public static string ConnectionString;
 
    protected void Application_Start()
    {
        bool.TryParse(WebConfigurationManager.AppSettings["ProxyServer"], out _useProxyServer);
        //end of add
        AreaRegistration.RegisterAllAreas();
        FilterConfig.RegisterGlobalFilters(GlobalFilters.Filters);
        RouteConfig.RegisterRoutes(RouteTable.Routes);
    }
}
```

## Modify Your Controller

​​You will need to add these lines to your controller:
- `IEnumerable<string> errorCodes;` 
- Adding parts after **&&** to `if (ModelState.IsValid && CMich.Web.Mvc.ReCaptcha.Validate(Request.Form["g-Recaptcha-Response"], MvcApplication.UseProxyServer, out errorCodes))`
- ```    else if (ModelState.IsValid)
    {
        ModelState.AddModelError("captchaFailed", "ReCaptcha check failed, please try again.");
    }```


```c#
// EXAMPLE
[HttpPost]
public ActionResult EmailForm(ViewModels.Home.EmailFormViewModel viewModel)
{
    IEnumerable<string> errorCodes;
 
    if (ModelState.IsValid && CMich.Web.Mvc.ReCaptcha.Validate(Request.Form["g-Recaptcha-Response"], MvcApplication.UseProxyServer, out errorCodes))
    {
        TempData["SuccessMessage"] = "Request successfully made.";
        return RedirectToAction("EmailForm", new { successMessage = "Request successfully made." });
    }
    else if (ModelState.IsValid)
    {
        ModelState.AddModelError("captchaFailed", "ReCaptcha check failed, please try again.");
    }
    return View(viewModel);
}
```

## Modify Your View.cshtml

​​You primarily need to add these lines to your Razor view:
- `<div class="g-recaptcha" data-sitekey="6Ld4EBsTAAAAADu8sU5wChc-gBHi7BZP_wyIdQMW"></div>` 
- `<script src='https://www.google.com/recaptcha/api.js'></script>​`

```html
<!-- // EXAMPLE -->
@using (Html.BeginForm(null, null, FormMethod.Post, new { id = "mainForm" }))
{
    @Html.ValidationSummary(false, "The following errors need addressed", new { role = "alert", @class = "alert alert-danger" })
 
    <div class="row">
        <div class="col-md-4">
            <div class="form-group">
                @Html.LabelFor(model => model.To)
                @Html.TextBoxFor(x => x.To, new { autocomplete = "off", @class = "form-control", aria_required = "true" })
                <span class="text-danger">
                    @Html.ValidationMessageFor(x => x.To)
                </span>
            </div>
        </div>
    </div>
    <div class="row">
        <div class="col-md-4">
            <div class="form-group">
                @Html.LabelFor(model => model.Subject)
                @Html.TextBoxFor(x => x.Subject, new { autocomplete = "off", @class = "form-control", aria_required = "true" })
                <span class="text-danger">
                    @Html.ValidationMessageFor(x => x.Subject)
                </span>
            </div>
        </div>
    </div>
    <div class="g-recaptcha" data-sitekey="6Ld4EBsTAAAAADu8sU5wChc-gBHi7BZP_wyIdQMW"></div>
    <button type="submit" class="btn btn-primary-cmich" id="submit">Submit Request</button>
 
}
```

```html
<!-- // EXAMPLE continued -->
@section Scripts
{​​
<script type="text/javascript">
     $(function () {
         $('#GraceHopper').focus();
     });
</script>
 
<script src='https://www.google.com/recaptcha/api.js'></script>
}
```

## Tags
[[reCaptcha]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ReCaptchaTag)
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)

