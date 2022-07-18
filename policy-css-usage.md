## Development / Deployment
​In development, all CSS must be written in a single custom SASS file. The file should be loaded after any other library CSS files in the `<head></head>` of the .html file.

For development purposes, SASS files must be compiled and the project must use the minified CSS file.

In staging, **ALL** custom written LESS files need to be compiled into a single minified CSS file.
If the CSS file will be reused on multiple projects, or if used for the styling of templates (such as SharePoint MasterPages and Page Layouts), the compiled CSS files need to be copied over to the CDN at the following location:

For Staging:
\\it-devweb1\WebApplications\api\Static\css\

For Production:
\\it-prodweb1\D$\inetpub\api\Static

Project files will need to be updated to point to the following location for CSS:
For Staging: http(s)://api2.cmich.edu/static/css

For Production:
\\it-prodweb1\D$\inetpub\api\Static

**Important Note**
Bootstrap LESS/SASS and CSS library files should never be modified. If you feel a modification needs to take place, the issue needs to be raised in a development team meeting. This will ease upgrading of the Bootstrap framework in the future.

## Stylesheet Rules
**ALWAYS** use external stylesheets. Do NOT write embedded stylesheets or use inline styles. External stylesheets provide an easier, more convenient and maintainable way to update styles.

Do NOT overwrite Bootstrap styles unless absolutely unavoidable. If you need to overwrite default bootstrap or application template behavior, define a custom class in a custom stylesheet and style accordingly.

All stylesheets should be written in SASS and compiled to minified CSS before use. Minification reduces file size, which in turn reduces load time.

All stylesheets should be maintained on git.

## File Name
CSS and SASS file names should be Pascal Case

Example: MyCssFile.sass
Example: MyCssFile.css

## Comments
There are 4 types of CSS comments: File-level, Section Heading, Multi-Line, Inline.

### File-level
This is used to provide file-level information at the top of every file.


File Header - This includes the Filename, Description, Version, Author and Department.

```
/*------------------------------------------------------------*\
    *Filename:  goDirectory.less/.css
     
    *Description:   LESS styles for the GoDirectory design
                     
    *Version:       1.0.0 (9/10/2015)
     
    *Author:        Jesse Earley
     
    *Department:    Office of Information Technology
\*------------------------------------------------------------*/
```

Table of Contents - This is used to provide a quick reference of Section Headings found in the file. These should exactly match the Section Headings found throughout the file. (The headings here are used for example only.)

```
/*------------------------------------------------------------*\
    TABLE OF CONTENTS
     
    *Variables                      -   Commonly used styles that can be readily updated
 
    *Mixins                         -   Commonly used properties
         
    *Site Search                    -   Styles for the "Site Search" page of the Directory
 
    *Student Profile Mini           -   Styles for the Student Profile Mini webpart
 
    *People and Department Search   - Styles for the People and Related Department page of the Directory
                                 
    *Media Queries          -   Styles for specific device widths
\*------------------------------------------------------------*/
```

### Section Heading
This is used to designate a section of styles. These should be grouped based on page structure(header, body, footer, etc.)

```
/*----- Media Queries -----*/
```

### Multi-Line
This is used when a long explanation is needed for a style.

```
/*
* Explanatory comment
* Can be multi-line
*/
```

### Inline
This is used when a short explanation is needed for a style.

```
.selector{
    color: #FFF //This is an inline comment
}
```

## Selectors
Selectors should be on a single line, with a space after the last selector, followed by an opening brace. A selector block should end with a closing curly brace that is not indented and on a separate line. A blank line should be placed between each selector block. Selectors should never be indented unless nesting within LESS occurs.

```
.selector {
 
}
 
.selector2 {
 
}
```

Multiple selectors should be on a seperate line with no space after each comma.

```
.selector1,
.selector2,
.selector3 {
}
```

### Property-Value Pairs

Property-value pairs should be listed starting on the line after the opening curly brace. Each pair should: 
*  Be on its own line 
*  Be indented one level
*  Have a single space after the colon that separates the property name from the property value 
*  End in a semicolon.
*  If multiple properties are defined in any given selector, those properties **MUST** be listed alphabetically.

```
.selector{
    name: value;
    name: value;
}
```

For properties with multiple values, separate each value with a single space following the comma(s).

```
font-family: Helvetica, sans-serif;
```

If a single value contains any spaces, that value must be enclosed within double quotation marks.

```
font-family: "Lucida Grande", Helvetica, sans-serif;
```

## Colors
When denoting color, ALWAYS use hexadecimal notation with capital letters. If it’s possible to specify the desired color using three-digit hexadecimal notation, always do so.

```
color: #FFF; /* Okay */
 
color: #FE9848; /* Okay */
 
color: #fff; /* Not okay */
```

## Dimensions
When denoting dimensions of an element or its margins, padding or borders, specify the units in either: em, px or %. If the value of the width or height is 0, do not specify units.

```
width: 12px; /* Okay */
 
width: 12%; /* Okay */
 
width: 12em; /* Okay */
 
width: 12rem; /* Okay */
 
width: 0; /* Okay */
 
width: 12; /* Not okay */
 
width: 0px; /* Not okay */
```

## SASS Guidelines
### Nesting
SASS will let you nest your CSS selectors in a way that follows the same visual hierarchy of your HTML. Be aware that overly nested rules will result in over-qualified CSS that could prove hard to maintain and is generally considered bad practice.

```
.panelTitle {
    color: #000;
    a {
        font-weight: bold;
    }
}
```

### Variables/Mixins
SASS variables/mixins must be in camel case format.

```
$theButtonColor: #FFF;
 
.theBox {
  height: 10px;
  width: 10px;
}
```


Variables/mixins should be used any time the same value, or same sets of values, are used for more than one element. These should always appear at the top of the stylesheet BEFORE any other styles. This allows for quick access to these shared styles in the event that they need to be changed or updated.


## Tags
[[CSS]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSSTag)
[[StyleGuidelines]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=StyleGuidelinesTag)
[[SASS]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=SASSTag)
[[LESS]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=LESSTag)
[[Bootstrap]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=BootstrapTag)
[[Deployment]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DeploymentTag)