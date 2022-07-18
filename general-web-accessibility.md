## ​​​​Dynamic Content

The W3C's ARIA specification refers to areas of a page that update dynamically without a refresh of the entire page as **live** regions. The dynamic nature of AJAX and dynamic content changes force assistive technologies to identify compartmentalized areas of the page that have changed, and to determine how and when users should be notified of changes that occur in these areas.

In these cases, the aria-live attribute should be used on the container element of the dynamic content.  

```html
<div aria-live="polite" id="resultsSection">
    &lt;h2&gt;Results&lt;/h2&gt;
    <div class="well sr-only">Person search results table. The table has 5 columns labelled as: Name, Position, Global ID, Campus ID and Action. </div>
    <div class="table-responsive">
        <table id="searchResultsTbl" class="table table-striped table-bordered"></table>
    </div>
</div>
```
Using aria-live="polite" will prompt a screen reader to notify a user once the content has been loaded and is visible on the page.  

## Forms​​

### Buttons  

*   <span style="line-height: 1.6;">​Buttons must have type="button" or type="submit".</span>  

*   <span style="line-height: 1.6;">When using an <input> tag for buttons, there must be a type, name and value attribue associated with the element.</span>
*   <span style="line-height: 1.6;">The value attribute for input buttons and the nested text for <button> elements will be read by screen readers when the button is accessed. These must **NEVER** be left empty.</span>
*   <span style="line-height: 1.6;">When a button should be used in place of an anchor, always use the <button> element. Do **NOT** style the <a> tag to make it look like a button.</span>

#### With ```<button>``` tag:
```html
<button type="button">This is a button</button>
```

#### ​​With ```<input>``` tag:  
```html
<input type="button" name="Button name" value="Click Here" / >
```

### ​Text Input Boxes  

*   <span style="line-height: 1.6;">​All text input fields need a "type" property of one of the following</span>  

*   <span style="line-height: 1.6;">password</span>
*   <span style="line-height: 1.6;">email</span>
*   <span style="line-height: 1.6;">text</span>
*   <span style="line-height: 1.6;">search</span>
*   <span style="line-height: 1.6;">tel</span>
*   <span style="line-height: 1.6;">url</span>

*   <span style="line-height: 22.4px;">​If the input is required for form completion, the <input> tag must have aria-required="true" and the required attribute.</span>
*   <span style="line-height: 22.4px;">​All text input fields need an id with associated label element. The label element needs a "for" attribute whose text matches the input id.</span><span style="line-height: 22.4px;">​</span>

#### Required Input Example with label:

```xml
@Html.LabelFor(x =&gt; x.ProxyName)
@Html.TextBoxFor(x =&gt; x.ProxyName, new { autocomplete = &quot;off&quot;, @class = &quot;form-control&quot;, aria_required = &quot;true&quot; })
&lt;span class=&quot;text-danger&quot;&gt;
     @Html.ValidationMessageFor(x =&gt; x.ProxyName)
&lt;/span&gt;
```

### Radio Buttons

*   <span style="line-height: 1.6;">​</span><span style="line-height: 1.6;">​​Fieldset and legend should only be used to associate groups of controls when a higher level description (i.e. the legend) is necessary. Single checkboxes or basic radio buttons (such as male/female for a gender group) that make sense from their labels alone do not requre a fieldset or legend. Nested fieldsets should generally be avoided.</span>  

*   <span style="line-height: 1.6;">All radio buttons must have type="radio".​​</span>

#### Radio Button Group Example:  

```html
<fieldset>
    <legend>Choose a shipping method:</legend>
    <input id="overnight" type="radio" name="shipping" value="overnight">
    <label for="overnight">Overnight</label><br>
    <input id="twoday" type="radio" name="shipping" value="twoday">
    <label for="twoday">Two day</label><br>
    <input id="ground" type="radio" name="shipping" value="ground">
    <label for="ground">Ground</label>
</fieldset>
```

#### Check Boxes

*   ​​​Fieldset and legend should only be used to associate groups of controls when a higher level description (i.e. the legend) is necessary. Single checkboxes or basic radio buttons (such as male/female for a gender group) that make sense from their labels alone do not requre a fieldset or legend. Nested fieldsets should generally be avoided

*   <span style="line-height: 1.6;">All check boxes n</span><span style="line-height: 1.6;">eed a type of "checkbox".</span>

#### Checkbox Group Example:
```html
<fieldset>
    <legend>Select your pizza toppings:</legend>
    <input id="ham" type="checkbox" name="toppings" value="ham">
    <label for="ham">Ham</label><br>
    <input id="pepperoni" type="checkbox" name="toppings" value="pepperoni">
    <label for="pepperoni">Pepperoni</label><br>
    <input id="mushrooms" type="checkbox" name="toppings" value="mushrooms">
    <label for="mushrooms">Mushrooms</label><br>
    <input id="olives" type="checkbox" name="toppings" value="olives">
    <label for="olives">Olives</label>
</fieldset>
```

#### Dropdown Lists
*   <span style="line-height: 1.42857;">​​To improve the accessibility of a list even further, when appropriate add .<span style="line-height: 1.42857;">optgroup </span><span style="line-height: 1.42857;">to group the options.</span></span>  

*   <span style="line-height: 1.42857;">​​​Do not confuse the <span style="line-height: 1.42857;">label </span><span style="line-height: 1.42857;">attribute of the </span><span style="line-height: 1.42857;">optgroup </span><span style="line-height: 1.42857;">element with the l</span><span style="line-height: 1.42857;">abel </span><span style="line-height: 1.42857;">element. They are very different things.</span></span>  

*   <span style="line-height: 1.42857;">​​​<span style="line-height: 1.42857;">It is recommended that multiple select menus be avoided. Not all browsers provide intuitive keyboard navigation for multiple select menus. Many users do not know to use CTRL/Command or Shift + click to select multiple items. Typically, a set of checkbox options can provide similar, yet more accessible functionality.</span></span>  

#### Dropdown Lists Example:
```html
<label for="favcity">Choose your favorite city?</label>
<select id="favcity" name="select">
    <option value="1">Amsterdam</option>
    <option value="2">Buenos Aires</option>
    <option value="3">Delhi</option>
    <option value="4">Hong Kong</option>
    <option value="5">London</option>
    <option value="6">Los Angeles</option>
    <option value="7">Moscow</option>
    <option value="8">Mumbai</option>
    <option value="9">New York</option>
    <option value="10">Sao Paulo</option>
    <option value="11">Tokyo</option>
</select>
```

#### File Upload

*   <span style="line-height: 1.6;"><span style="line-height: 1.42857;">Upload buttons must be made with an <input> tag and have type="file".</span></span>  

#### Labels

*   ​​​​<span style="line-height: 1.42857;">Use that standard label for the input as the screen reader will read the associated label automatically so long as you have the for attribute on the label that matches the id of the input.</span><span style="line-height: 1.42857;">​</span>

*   <span style="line-height: 1.42857;">Refer to the previous examples to see how <label> should be used.</span>

#### Addons

*   <span style="line-height: 1.6;">​​Addons refers to the Bootstrap usage of addons. Refer to the official Bootstrap documentation to find more detailed examples of addons across various Bootstrap versions.</span>  

*   ​If using input addons, ensure the associated label indicates what the addons are portraying.

#### Addon Example:
```html  
<div class="input-group">
  <span class="input-group-addon" id="basic-addon1">@</span>
  <input type="text" class="form-control" placeholder="Username" aria-describedby="basic-addon1">
</div>
```

#### Disabled State

*   Disabled elements must have the "disabled" attribute.

*   If disabling all controls in a fieldset, add the disabled attribute to the fieldset.

### Help Text (aria-describedby)

*   <span style="line-height: 1.6;">​Help text needs id text that matches the input aria-described by text.</span>  

#### Help Text Example:
```html
<div aria-describedby="info">
    <p id="info">This is a paragraph</p>
</div>
```

## Tables​

​Tables must have a title using an ```<h2>```  heading tag located just above the table. Immediately following the opening ```<table>``` tag, the ```<caption>``` must be used to provide a description of the table content. If  you do **not **​want this description to be visible, add the class "sr-only​-tableCaption" to the caption. The ```<caption class="well">``` with description must be present whether or not you choose to use the "sr-only" class.

### With .sr-only-tableCaption
```html
&lt;h2&gt;Table Title&lt;/h2&gt;
<table>
    <caption class="well sr-only-tableCaption">Short description of table.</caption>
    <thead>

    </thead>
    <tbody>

    </tbody>
</table>
```
### ​​​Witho​ut .sr-only  
```html
&lt;h2&gt;Table Title&lt;/h2&gt;
<table>
    <caption class="well">Short description of table.</caption>
    <thead>

    </thead>
    <tbody>

    </tbody>
</table>
```
### Identify Row and Column Headers

A critical step toward creating an accessible data table is to designate row and/or column headers. In the markup, the <td>element is used for table data cells and the <th> element is used for table header cells. Table headers should never be empty.

#### Scope Attribute  

The scope attribute identifies whether a table header is a column header or a row header.
```html
<table>
    <caption class="well sr-only">
        This is a description of the contents of the table.
    </caption>
    <thead>
        <tr>
            <th scope="col">Name</th>
            <th scope="col">Age</th>
            <th scope="col">Birthday</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Jackie</th>
            <td>5</td>
            <td>April 5</td>
        </tr>
        <tr>
            <th scope="row">Beth</th>
            <td>8</td>
            <td>January 14</td>
        </tr>
    </tbody>
</table>
```
The scope attribute tells the browser and screen reader that everything within a column that is associated to the header with scope="col" in that column, and that a cell with scope="row" is a header for all cells in that row.  

## Alerts

All alerts must have role="alert". When this role is added, the browser will send out an accessible alert event to assistive technology products which can then notify the user about the alert.​​

```html
<div class="alert alert-info" role="alert">
    This is an alert.
</div>
```

## ​Links

Links should be descriptive and not open to interpretation. Links should also include the title attribute.  

```html
<a href="http://wwww.cmich.edu" title="www.cmich.edu">This is a link to the CMU Homepage</a>
```
## Icons​  

Screen readers will not correctly interpret icons, so they must be hidden from them. The <i> element should have "aria-hidden=true". Additionally, add a <span> element following the <i> element with the "sr-only" class that the screen reader can accurately read.
```html
<i aria-hidden="true" class="icon-cmich-search"></i>
<span class="sr-only">search</span>
```  

## Images

*   <span style="line-height: 1.6;">​All images need alt tags that briefly describe the content of the image. </span>  

*   <span style="line-height: 1.6;">Images that are decorative, or convey no real message still need an empty string ("") for an alt attribute. Without this, screen readers may read the image location to the user.</span>

*   <span style="line-height: 1.6;">Avoid using both alt and title attributes on the same image tag. This is a common mistake where the developer will use both, with the same text in both. The result is that the screen reader will read both, which is repetitive.</span>

*   <span style="line-height: 1.6;">More about the title attribute. There seems to be some confusion around SEO around title attributes. While search engines do crawl title *tags* in web pages, they do not crawl title *attributes* of tags. The only thing a title attribute does is makes text appear on mouse over as a tooltip.</span>

``` html
<img src='image.jpg' alt='Image Alt Text'/>
```

## Tags
[[​Accessibility]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=AccessibilityTag)
[[HTML]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=HTMLTag)
[[WebDesign]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=WebDesignTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)

