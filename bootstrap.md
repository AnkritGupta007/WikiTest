Note: DO NOT overwrite Bootstrap styles unless absolutely unavoidable (talk to Jesse/Josh first). If needed, define a custom class and style accordingly.

## Container

The root element of the Bootstrap grid system is the container. There are 2 types of containers: **.container** (fixed-width) and **.container-fluid** (full-width).  

</span></span>

## Row  

Rows must be placed within a container but do not need to be direct children.  

## Columns

Rows can **ONLY** have columns as immediate children but rows do not need to be parents of columns. NOTE: If a column is not contained within a row, there will be a left and right padding of 15px.  

<strong>Okay:</strong>

```html
<div class="container-fluid"> 
      <div class="row"> 
            <div class="col-md-12"> </div> 
      </div> 
</div>
```

<strong>Not Okay:</strong>
```html
<div class="container">
    <div class="row">
        <div class="col-md-3"></div>
        <p>This is wrong. Only columns can be children of rows.</p>
    </div>
</div>
```

<strong>Not Okay:</strong>
```html
<div class="row"> <!-- Rows must be within a container -->
    <div class="container">
    </div>
</div>
```

## Tables

*   <span><span>When using a table to present tabular data and when the table is going to be more than one row, use the **.table-striped** class.</span></span>

```html
<table class="table table-striped">
    <thead>
        <tr>
            <th>Firstname</th>
            <th>Lastname</th>
            <th>Email</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>John</td>
            <td>Doe</td>
            <td>john@example.com</td>
        </tr>
        <tr>
            <td>Mary</td>
            <td>Moe</td>
            <td>mary@example.com</td>
        </tr>
        <tr>
            <td>July</td>
            <td>Dooley</td>
            <td>july@example.com</td>
        </tr>
    </tbody>
</table>
```

*   When building for mobile, consider using **.table-condensed** class to cut cell padding in half and/or **.table-responsive** class to add horizontal scroll to the table on smaller screens.

```html
<div class="table-responsive">
    <table class="table table-condensed">
        <thead>
            <tr>
                <th>Firstname</th>
                <th>Lastname</th>
                <th>Email</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>John</td>
                <td>Doe</td>
                <td>john@example.com</td>
            </tr>
            <tr>
                <td>Mary</td>
                <td>Moe</td>
                <td>mary@example.com</td>
            </tr>
            <tr>
                <td>July</td>
                <td>Dooley</td>
                <td>july@example.com</td>
            </tr>
        </tbody>
    </table>
</div>
```

<span>

## Forms

</span><span>

<span>For all form development, unless a designer is involved as part of the project (and the forms involved with the project are special case), the Bootstrap framework and the default styling (vertical form layout) should be used. The information below are the agreed upon standards for how a form should be constructed.</span> Reference: [http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)

</span>

*   <span>NOTE: When similar input can be grouped in a horizontal format, it is okay to do so. For example, First Name, Middle Name and Last Name input boxes could be in a horizontal format.</span>
*   <span><span><span>Form elements **MUST** have the .form-control</span></span> class.  
    </span>

<span>

Example usage:

Please refer to the [Application Template Forms Page](http://cdn.cmich.edu/css/applicationTemplate/demo/applicationTemplateFormPage.html) for examples.  

</span><span>

### Field Labels

</span>

*   Each input field should have a corresponding label **ABOVE** the input.
*   Since we require the label to be above the input, the .form-horizontal (do not confuse .form-horizontal with .form-inline) class should be used sparingly (if ever).

### Input Boxes

*   Input boxes must always include placeholder text.
*   Input boxes should not be wider than the potential input text (generally col-md-6).
*   Reference: [http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)

```html
<input class="form-control" type="text" placeholder="Text input" />
```

### Text Areas

*   <span>Text areas must expand the full width of the form</span>
*   <span>Text areas should be at least 3 rows, but no more than 7</span>
*   <span>Reference: [http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)</span>

### Checkboxes and Radio Buttons

*   <span>If there are more than 3 checkboxes or radio buttons, the checkboxes or radio buttons should be stacked vertically</span>
*   <span>If there are 3 or less checkboxes and radio buttons, the checkboxes and radio buttons should appear in-line if appropriate, otherwise they should be stacked vertically</span>
*   <span><span>Reference: [http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)</span></span>

### Selects

*   <span>Default Bootstrap behavior should be used for selects.</span>
*   <span><span><span><span>Reference: [http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)</span></span></span></span>

### Form Control Add-Ons

<span></span><span></span>  

*   <span><span>Form control add-ons allow for prepended and appended text to an input</span></span>
*   The following add-ons are recommended:

*   Currency-

*   Preappend - **$**
*   Append - **.00**

*   Email Address

*   Append - **@cmich.edu**

*   URL's -

*   Append - **http://** or **https://**

*   Reference:<span><span><span><span><span>[ http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)</span></span></span></span></span>

<span></span><span>

```html
<div class="input-group">
    <span class="input-group-addon">$</span>
    <input class="form-control" id="appendedPrependedInput" placeholder="Emter dollar amount"/>
    <span class="input-group-addon">.00</span>
</div>
```

### Disabled Fields

</span>

*   <span>Default Bootstrap behavior should be used for disabled fields</span><span><span><span>.</span></span></span>
*   <span><span><span>Reference: [http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)</span></span></span>

<span>

## Help Text/Tooltip

*   Where appropriate, help text/tooltips should be used on form elements that may need additional explanation
*   <span class="ms-rteThemeForeColor-2-0">The icon that should be used for denoting help text/tooltips is the cmich icon</span> **<span class="mls">.icon-cmich-question-6</span>** <span class="ms-rteThemeForeColor-2-0">(</span><span class="ms-rteThemeForeColor-2-0">http://cdn.cmich.edu/Fonts/cmichicons/demo.html)</span>  

*   Reference: [http://getbootstrap.com/javascript/#tooltips](http://getbootstrap.com/javascript/#tooltips)

```html
<a href="#" data-toggle="tooltip" title="first tooltip"><i class="icon-cmich-question-6"></i></a>
```

## Buttons

*   If using the [Application Template](http://cdn.cmich.edu/css/applicationTemplate/demo/applicationTemplate.html), all primary action buttons should use the .btn-primary-cmich. Otherwise, Bootstrap's **.btn-primary** class should be used.  

*   All other form buttons should use the Bootstrap's **.btn-default** class.​
*   Reference: [http://getbootstrap.com/css/#buttons](http://getbootstrap.com/css/#buttons)

```html
<button class="btn btn-primary-cmich" type="button">Maroon Button</button> 

<button class="btn btn-primary" type="button">Primary Button</button>
```

## Alerts

*   There are 3 types of alerts that should be used with forms:

*   **Error** - Error alerts must appear at the top of the form, focus must be set to the alert
*   **Success** - Success alerts must appear at the top of the form, focus must be set to the alert
*   **Information** - Information alerts can appear anywhere on the form, and should always be visible. These can be used for such things as disclaimers

*   Reference: [http://getbootstrap.com/components/#alerts](http://getbootstrap.com/components/#alerts)

```html
<div class="alert alert-success">Well done!</div>
```

## Validation Labels

*   Bootstrap **Warning** labels should be used for failed validation on form fields
*   Reference: [http://getbootstrap.com/components/#labels](http://getbootstrap.com/components/#labels)

## Modal

There are three different sizes of Bootstrap modals.

NOTE: All sizes will fit on all screen sizes. In essence, a small modal will be the same width as a large modal on a small screen.  

Small (**.modal-sm**):

</span>

*   Use sparingly, but also in cases where there is very little content to display.  

<span>

Medium (**.modal**):

</span>

*   Use in most circumstances unless the content generates a scroll bar or <span>significant</span> white-space occurs below the content.  

<span>

Large (**.modal-lg**):

</span>

*   Use sparingly, but in cases where there is a significant amount of content to display.

## Navigation

Typically Bootstrap styles are not overriden, instead, custom classes are used. However, one instance where Bootstrap needs to be overridden is with the Bootstrap Navigation collapse. To overrride the default navigation closure at 768px, the following styles need to be used:

```css
@media (min-width: 768px) and (max-width: 991px) {
    .navbar-collapse.collapse {
        display: none !important;
    }
    .navbar-collapse.collapse.in {
        display: block !important;
    }
    .navbar-header .collapse,
    .navbar-toggle {
        display: block !important;
    }
    .navbar-header {
        float: none;
    }
}
```

The "max-width" value needs to be changed to whatever width the navigation needs to collapse.  

## Additional References  

<span>

For additional reference, documentation and practice, please refer to the following sites:

[http://www.w3schools.com/bootstrap/default.asp](http://www.w3schools.com/bootstrap/default.asp)

[http://getbootstrap.com/css/](http://getbootstrap.com/css/)

[](http://getbootstrap.com/css/)[http://getbootstrap.com/components/](http://getbootstrap.com/components/)  

</span>

## Tags
[[BootStrap]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=BootStrapTag)
[[HTML]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=HTMLTag)
[[CSS]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSSTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
