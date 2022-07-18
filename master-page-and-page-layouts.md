## Master Page Usage/Creation  

The CMU SharePoint 2013 Environment uses a single SharePoint Master Page called: CMichMasterPage.

## How to set up​ Master Page for Page Layout  

In the master page HTML, search for "ContentPlaceHolderMain" and add class "container" to the div as show.

```html
<div data-name="ContentPlaceHolderMain" class="container">
```  

## Generating a Page Layout

Go to design manager and click "Edit Page Layouts" on the left side of the page. Click on "Create a page layout" to open a box where you can create a page layout. Type a name in the first textbox, make sure the correct master page is selected, and select the proper content type. Click okay when finished.

## Designing the Page Layout

<span>Download a copy of the page layout HTML to edit the layout.</span> The page layout should have Bootstrap fluid rows and columns as a grid to hold page content. Because the master page has a "container" around the placeholder for page layouts, width of the content will match the rest of the master page.

<span>At the bottom of the body section there are snippets for page fields and other items. These can be placed within Bootstrap styled elements to change the placement of these elements on the page.</span>

## Tags
[[SharePoint]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SharePointTag)
[[WebDesign]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=WebDesignTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
