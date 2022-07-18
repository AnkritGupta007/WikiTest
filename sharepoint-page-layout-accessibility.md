## ​Background

It is important for the CMU website to not only be accessible to a multitdude of devices, but to those that have some form of vision impairement as well. A typical tool used by those with vision impairement is a screen reader. The following information will help ensure that your SharePoint Page Layouts are accessible and can be navigated successfully by a screen reader.  

## Navigation  

Navigation within SharePoint typically uses a combination of default SharePoint navigation controls and Bootstrap markup to make those navigation controls collapsable. With collapsable elements, it's important to convey to the screen reader whether such an element is in fact collapsed or expanded. To accomplish this, the following markup needs to be in place for Top/Side navigations that collapse for mobile:  
```html
<nav class="navbar" role="navigation" aria-label="primary">
	<div class="container">
		<!-- Brand and toggle get grouped for better mobile display -->
		<div class="navbar-header">
			<button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#nav-collapse-local" aria-label="Expand and collapse primary site navigation" aria-expanded="false">
				<span class="sr-only">Toggle navigation</span>
				<span class="icon-bar"></span>
				<span class="icon-bar"></span>
				<span class="icon-bar"></span>
			</button>
		</div>

		<!-- Collect the nav links, forms, and other content for toggling -->
		<div class="collapse navbar-collapse nav-collapse-local" id="nav-collapse-local">
			<div data-name="QuickLaunch">
				<div id="sideNavBox" class="ms-dialogHidden ms-forceWrap ms-noList">
					<SharePoint:AjaxDelta ID="DeltaPlaceHolderLeftNavBar" BlockElement="true" CssClass="ms-core-navigation" runat="server">
						<div>
							<designertempnode name="PlaceHolderLeftNavBarTop" />
							<designertempnode name="PlaceHolderQuickLaunchTop" />
							<designertempnode name="PlaceHolderLeftNavBarDataSource" />
							<designertempnode name="PlaceHolderCalendarNavigator" />
							<designertempnode name="PlaceHolderLeftActions" />
							<SharePoint:SPNavigationManager ID="QuickLaunchNavigationManager" runat="server" QuickLaunchControlId="v4QuickLaunchMenu" ContainedControl="QuickLaunch" EnableViewState="false">
								<sharepoint:delegatecontrol runat="server" controlid="QuickLaunchDataSource">
									<template_controls>
										<PublishingNavigation:PortalSiteMapDataSource runat="server" ID="SiteMapDS" SiteMapProvider="CurrentNavigation" EnableViewState="false" StartFromCurrentNode="true" ShowStartingNode="false" TrimNonCurrentTypes="Heading">
										</PublishingNavigation:PortalSiteMapDataSource>
									</template_controls>
								</sharepoint:delegatecontrol>
								<SharePoint:AspMenu ID="V4QuickLaunchMenu" runat="server" EnableViewState="false" DataSourceId="QuickLaunchSiteMap" UseSimpleRendering="true" Orientation="Vertical" StaticDisplayLevels="3" AdjustForShowStartingNode="true" MaximumDynamicDisplayLevels="0" SkipLinkText="">
								</SharePoint:AspMenu>
							</SharePoint:SPNavigationManager>
							<designertempnode name="PlaceHolderQuickLaunchBottom" />
						</div>
					</SharePoint:AjaxDelta>
				</div>
			</div>
		</div>
	</div>
</nav>
```
Please Note: Both your 'data-target' value and 'id' may differ than the one listed in the above example.

### ```<nav>``` Element  

There are two key pieces to take note of in this code. First, the ```<nav>``` element:  
```html
<nav class="navbar" role="navigation" aria-label="primary">
```

The ```<nav>``` element needs both the **role** and **aria-label** attributes.

**role** must always have the value of "**navigation**".

**aria-label** must have one of two values:

*   If your website **ONLY** has one navigation (either top or side), this value needs to be "**primary**"

*   **Ex: aria-label="primary"**

*   If your website has **BOTH** a top and side navigation, the top navigation needs the value of "**primary**" and the side navigation needs a value of "**secondary**"

*   **Ex: aria-label="primary", aria-label="secondary"**

### ```<button>``` element  

The second piece to take note of is the button:  
```html
<button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#nav-collapse-local" aria-label="Expand and collapse primary site navigation" aria-expanded="false">
	<span class="sr-only">Toggle navigation</span>
	<span class="icon-bar"></span>
	<span class="icon-bar"></span>
	<span class="icon-bar"></span>
</button>
```

**'aria-label'** needs the value of: "**Expand and collapse ___ site navigation**"

This blank line needs to be filled in with one of two values:

*   If your website **ONLY** has one navigation (either top or side), this value needs to be "**primary**"

*   **Ex: "Expand and collapse primary site navigation"**

*   If your website has **BOTH** a top and side navigation, the top navigation needs the value of "**primary**" and the side navigation needs the valued of "**secondary**"

*   **Ex: "Expand and collapse primary site navigation", "Expand and collapse secondary site navigation"**

Additionally, the **<span class="sr-only">Toggle navigation</span>** must also be present within the button. The "**sr-only**" class is a Bootstrap class for screen reader accessibility.

### JavaScript  

The navigation markup works in conjuction with the following JavaScript (which is already included via the MasterPage) to change the state of the collapsable element on click so that it is read by the screenreader.  
```javascript
//All collapsable navs
$(".navbar-toggle").click(function () {
	if ($(this).attr("aria-expanded") == "false") {
		$(this).attr("aria-expanded", "true");
	}
	else {
		$(this).attr("aria-expanded", "false");
	}
});
```

## Breadcrumb

The following is an example of breadcrumb navigation markup:  
```html
<div id="breadCrumb" class="breadcrumb noindex breadCrumb" aria-label="breadcrumb" role="navigation">
	<asp:sitemappath runat="server" sitemapproviders="SPSiteMapProvider,SPXmlContentMapProvider" rendercurrentnodeaslink="false" hideinteriorrootnodes="true" rootnodestyle-cssclass="cmich-homeLink">
	</asp:sitemappath>
</div>
```

<span><span>The breadcrumb container element needs both the **role** and **aria-label** attributes.</span></span>

**role** must always have the value of "**navigation**".

**aria-label** must have the value of "**breadcrumb**".  

## Page Title

The following is an example of page title markup:
```html
<h1 data-name="Page Field: Title">
	<PageFieldTextField:TextField ID="TextField1" FieldName="fa564e0f-0c70-4ab9-b863-0177e6ddd247" runat="server">
	</PageFieldTextField:TextField>
</h1>
```

The page title should be wrapped in an **<h1>** element to denote proper heirarchy on the page for the screen reader.

## Site Title

The following is an example of site title markup (primarily used at the t​​​op of side navigations):
```xml
&lt;h2 data-name=&quot;SiteTitle&quot;&gt;
	&lt;SharePoint:AjaxDelta ID=&quot;AjaxDelta2&quot; runat=&quot;server&quot;&gt;
		&lt;SharePoint:SPLinkButton ID=&quot;SPLinkButton2&quot; runat=&quot;server&quot; NavigateUrl=&quot;~site/&quot;&gt;
			&lt;SharePoint:ProjectProperty ID=&quot;ProjectProperty3&quot; Property=&quot;Title&quot; runat=&quot;server&quot;&gt;
			&lt;/SharePoint:ProjectProperty&gt;
		&lt;/SharePoint:SPLinkButton&gt;
	&lt;/SharePoint:AjaxDelta&gt;
&lt;/h2&gt;
```
<span>The site title should be wrapped in an **<h2>** element to denote proper heirarchy on the page for the screen reader.</span>

## Presentational Images

If using presentation images that are defined as background images in CSS, use the "sr-only" class to define what that element is:
```html
<div class="presBanner">
	<a title="Office of the President" href="//www.cmich.edu/president/">
		<div class="presBannerImage"></div>
		<div class="presBannerImageMobile"></div>
		<span class="sr-only">Office of the President Banner</span>
	</a>
</div>
```
In the example above, the banner image for the President website is defined using ```<div>``` elements, and the image is applied as a background image via CSS. Note the ```<span class="sr-only">Office of the President Banner</span>``` within the banner container has a text description of what that image is. This will be read by a screen reader.

## Icons

Screen readers will **NOT** be able to interpret icon based fonts (ex: CMich Icons, Font Awesome, etc.). Below is an example on how to remedy this:
```html
<div class="facebookButton">
	<i aria-hidden="true" class="icon-cmich-facebook"></i>
	<span class="sr-only">Facebook Icon</span>
</div>
```
<span><span>The ```<i>``` element needs the **aria-hidden** attribute with a value of "**true**". This will tell the screen reader to simply skip over this element.  
</span></span>

Below the ```<i>``` element, the "**sr-only**" class needs to be applied to a ```<span>``` element, with the content of the span being a text description of the icon.

## Tags
[[Accessibility]](https://code.cmich.edu/search?project_id=365&scope=wiki_blobs&search=AccessibilityTag)
[[HTML]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=search=HTMLTag)
[[WebDesign]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=WebDesignTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
