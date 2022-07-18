<div class="alert alert-info">The following guidelines should be followed for all custom CSS and LESS files written for web designs and internal applications. The only exceptions should be in-line styles or internal stylesheets where following these guidelines may not always be possible.​</div>

## Stylesheet Rules  

**ALWAYS** use external stylesheets. **Do NOT** write embedded stylesheets or use inline styles. External stylesheets provide an easier, more convenient and maintainable way to update styles.

**Do NOT** overwrite Bootstrap styles unless absolutely unavoidable (Talk to Jesse / Josh first). If needed, define a custom class and style accordingly.  

**All** stylesheets should be written in LESS and compiled to minified CSS before use. <span>Minification reduces file size, which in turn reduces load time.</span>

**All** stylesheets should be maintained behind version control (Vault)

<span>

## File Name

CSS and LESS file names should be Pascal Case  

<span><span>Example: MyCssFile.less</span></span>  
Example: MyCssFile.css  

</span>

## Comments

There are 4 types of CSS comments: **File-level,** ****Sectio**n Heading, Multi-Line, Inline**.

### File-level

This is used to provide file-level information at the top of every file.

*   **File Header** - This includes the Filename, Description, Version, Author and Department.

```html
/*------------------------------------------------------------*\
	*Filename:	goDirectory.less/.css
	
	*Description: 	LESS styles for the GoDirectory design
					
	*Version:		1.0.0 (9/10/2015)
	
	*Author:		Jesse Earley
	
	*Department:	Office of Information Technology
\*------------------------------------------------------------*/
```

*   **Table of Contents** - This is used to provide a quick reference of Section Headings found in the file. These should exactly match the Section Headings found throughout the file. (The headings here are used for example only.)

```html
/*------------------------------------------------------------*\
	TABLE OF CONTENTS
	
	*Variables                      -   Commonly used styles that can be readily updated

    *Mixins                         -   Commonly used properties
        
    *Site Search                    -   Styles for the "Site Search" page of the Directory

    *Student Profile Mini           -   Styles for the Student Profile Mini webpart

    *People and Department Search   - Styles for the People and Related Department page of the Directory
								
	*Media Queries  		-	Styles for specific device widths
\*------------------------------------------------------------*/
```

### Section Heading

<span class="ms-rteThemeForeColor-2-0">This is used to designate a section of styles. These should be grouped logically (header, body, footer, etc.)</span>

```html
/*-----	Media Queries -----*/
```

### Multi-Line

This is used when a long explanation is needed for a style.  

```html
/*
* Explanatory comment
* Can be multi-line
*/
```

### Inline

This is used when a short explanation is needed for a style.  

```css
.selector{
    color: #FFF //This is an inline comment
}
```

## Selectors

Selectors should be on a single line, with a space after the last selector, followed by an opening brace. A selector block should end with a closing curly brace that is not indented and on a separate line. A blank line should be placed between each selector block. Selectors should never be indented unless nesting within LESS occurs.

```css
.selector {

}

.selector2 {

}
```

Multiple selectors should be on a seperate line with no space after each comma.

```css
.selector1,
.selector2,
.selector3 {
}
```

<span class="ms-rteThemeForeColor-2-0"></span><span class="ms-rteThemeForeColor-2-0"></span>

## <span class="ms-rteThemeForeColor-2-0">Property-Value Pairs  
</span>

<span class="ms-rteThemeForeColor-2-0">Property-value pairs should be listed starting on the line after the opening curly brace. Each pair should: be on its own line, be indented one level, have a single space after the colon that separates the property name from the property value and <span class="ms-rteThemeFontFace-1 ms-rteThemeForeColor-2-0">end in a semicolon.</span></span>

```css
.selector{
    name: value;
    name: value;
}
```

<span class="ms-rteThemeForeColor-2-0">For properties with multiple values, separate each value with a single space following the comma(s).</span>

```css
font-family: Helvetica, sans-serif;
```

If a single value contains any spaces, that value must be enclosed within double quotation marks.

```css
font-family: "Lucida Grande", Helvetica, sans-serif;
```

<span class="ms-rteThemeForeColor-2-0">If multiple properties are defined in any given selector, those properties **MUST** be listed alphabetically.  
</span>

## <span class="ms-rteThemeForeColor-2-0">Colors</span>

<span class="ms-rteThemeForeColor-2-0">When denoting color, **ALWAYS** use hexadecimal notation with capital letters. If it’s possible to specify the desired color using three-digit hexadecimal notation, always do so.</span>

```css
color: #FFF; /* Okay */

color: #FE9848; /* Okay */

color: #fff; /* Not okay */
```

## <span class="ms-rteThemeForeColor-2-0">Dimensions</span>

<span class="ms-rteThemeForeColor-2-0">When denoting dimensions of an element or its margins, padding or borders, specify the units in either: em, px or %. If the value of the width or height is 0, do not specify units.</span>

```css
width: 12px; /* Okay */

width: 12%; /* Okay */

width: 12em; /* Okay */

width: 12rem; /* Okay */

width: 0; /* Okay */

width: 12; /* Not okay */

width: 0px; /* Not okay */
```

## <span class="ms-rteThemeForeColor-2-0">LESS Guidelines  
</span>

### Nesting

<span class="ms-rteThemeForeColor-2-0">LESS will let you nest your CSS selectors in a way that follows the same visual hierarchy of your HTML. Be aware that overly nested rules will result in over-qualified CSS that could prove hard to maintain and is generally considered bad practice.</span>

```css
.panelTitle {
    color: #000;
    a {
        font-weight: bold;
    }
}
```

### Variables/Mixins  

<span class="ms-rteThemeForeColor-2-0">LESS variables/mixins must be in camel case format.</span>

```css
@theButtonColor = #FFF;

.theBox {
  height: 10px;
  width: 10px;
}
```

<span class="ms-rteThemeForeColor-2-0">Variables/mixins should be used any time the same value, or same sets of values, are used for more than one element. These should always appear at the top of the stylesheet **BEFORE** any other styles. This allows for quick access to these shared styles in the event that they need to be changed or updated.</span>

## Tags
[[CSS]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSSTag)
[[WebDesign]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=WebDesignTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
