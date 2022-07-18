For all of the following rules, refer to the current application template demo at: [http://cdn.cmich.edu/css/applicationTemplate/demo/applicationTemplate.html](http://cdn.cmich.edu/css/applicationTemplate/demo/applicationTemplate.html) then view the page source OR get the application template project from vault at Designs/CMich.ApplicationTemplateBootstrap3MVC​. The application template only refers to the wrapper of the application (header, footer(s), primary navigation, side navigation, banner) and, for the most part, should be used as is without modification. Any modifications of the application template code MUST be confirmed by Jesse and/or Josh. For the content of the application, refer to the [General Web Accessibility](/sites/it/WebTeam/wiki/Documentation/Pages/General%20Web%20Accessibility.aspx) documentation page.​​

## ​Primary Navigation  

### Dropdown Button  

When using a dropdown button, the button needs an aria-haspopup="true" and an aria-expanded="false".

The button element should contain two span elements, one for the caret and one for the description of the button that has a class of "sr-only".

The buttons (if links) should use an "onclick" property to access the href property that an anchor would otherwise use.​

Example:

```html
<div class="btn-group navbar-btn">
	<button type="button" class="btn btn-primaryNav" onclick="location.href='#'">Link 1</button>
	<button type="button" class="btn btn-primaryNav dropdown-toggle" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
		<span class="caret"></span>
		<span class="sr-only">Link 1 dropdown</span>
	</button>
	<ul class="dropdown-menu">
		<li><a href="#">Action</a></li>
		<li><a href="#">Another action</a></li>
		<li><a href="#">Something else here</a></li>
		<li role="separator" class="divider"></li>
		<li><a href="#">Separated link</a></li>
	</ul>
</div>
```

### Non-​​​​dropdown Button

```xml
&lt;button type=&quot;button&quot; class=&quot;btn btn-primaryNav btn-noDropdown&quot; onclick=&quot;document.location=&#39;@Url.Action(&quot;Create&quot;)&#39;&quot;&gt;Link 2&lt;/button&gt;
```

### Search Box
The search box will read as a table element when using ​​the Macintosh screen reader using Firefox and El Capital OS. This is a known issue.

​When using the search box, wrap the search in a <form> element with role="search".

```html
<form class="navbar-form navbar-right searchMenu" role="search">
	<div class="input-group">
		<input type="search" aria-label="Search Box" class="form-control searchBox" title="Search Box" accesskey="S" maxlength="2048" placeholder="Search...">
		<span class="input-group-btn">
			<button title="Search Button" aria-label="Search Button" type="button" class="btn btn-default btn-search" id="SearchButtonDirectory"><i aria-hidden="true" class="icon-cmich-search"></i></button>
		</span>
	</div>
</form>
```  

## Secondary Navigation​​

Support for secondary navigation has been removed from the Application Template. All use of navigation to this point in applications using the Application Template have solely used the "Primary Navigation". If you are in need of a secondary navigation, let one of the designers know.<span style="color: #0072c6; font-family: &quot;roboto slab&quot;, serif; font-size: 30px; line-height: 1.4;"></span>

## Side Navigation

When using the Side Navigation, it must have an "aria-label="side navigation" on the div with the "sidebar-nav" class (Line 1 in the following example).  

The expand button in the mobile view should have an .sr-only description explaining the interaction of the button (<span style="line-height: 22.4px;">Line 6 in the following example)</span>.

```html
<div class="sidebar-nav" aria-label="side navigation">
	<nav class="navbar navbar-default navbar-side" role="navigation">
		<div class="navbar-header">
			<h3 class="navbar-brand margin0">Sidebar menu</h3>
			<button type="button" class="navbar-toggle navbar-toggle-sideNav btn btn-top btn-gold" data-toggle="collapse" data-target=".sidebar-navbar-collapse" aria-label="Expand and collapse side site navigation">
				<span class="sr-only">Toggle navigation</span>
				<span class="icon-bar"></span>
				<span class="icon-bar"></span>
				<span class="icon-bar"></span>
			</button>
		</div>
		<div class="navbar-collapse collapse sidebar-navbar-collapse">
			<ul class="nav navbar-nav" role="menubar">
				<li><a href="#">Menu Item 1</a></li>
				<li><a href="#">Menu Item 2</a></li>
				<li>
					<a href="#">Menu Item 3</a>
					<ul class="navbar-nav-sub">
						<li><a href="#">Sub Menu Item 1</a></li>
						<li><a href="#">Sub Menu Item 2</a></li>
					</ul>
				</li>
				<li><a href="#">Menu Item 4</a></li>
			</ul>
		</div>
	</nav>
</div>
```

## Application Footer

When using the Application Footer, it must have an aria-label="Application Footer" (Line 1 in the following example).  

```html
<ul role="group" aria-label="Sample Header Link Group1">
     <li><a href="#">Example Link</a></li>
     <li><a href="#">Example Link</a></li>
</ul>
```​  

If the header is not descriptive enough, each link group should  have an aria-label briefly explaining the contents of the group.

```html
<div class="col-xs-4">
	<div class="appFooterCol">
		<h4>Contact</h4>
		<ul role="group" aria-label="Links to pages with contact information">
			<li><a href="#">Emergency</a></li>
			<li><a href="#">Registration</a></li>
		</ul>
	</div>
</div>
```

## Page Footer

The page footer should use the <footer> element and have a role="contentinfo".  

```xml
<footer class="pageFooter" role="contentinfo">

</footer>
```

## Tags
[[​Accessibility]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=​AccessibilityTag)
[[HTML]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=HTMLTag)
[[WebDesign]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=WebDesignTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
