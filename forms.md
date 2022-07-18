For all form development, unless a designer is involved as part of the project (and the forms involved with the project are special case), should be created with the Bootstrap framework and the default styling. The information below are the agreed standards for how a form should be constructed.  

## Layout

*   Form layout should be vertical in nature (Bootstrap default)

*   <span>If a form has multiple logical groupings of data, the form should be split up into multiple pages (ie. a wizard), with each step of the wizard coinciding with each grouping of data. Please refer to the [[Multi-Step Wizard Interfaces]] page for more information.  
    </span>

*   Reference: [http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)

Example usage:

Confirmation pages (if your form has one), should be laid out in the same manner, with the only exception being using a <div> to surround the user selection/input rather than an input control.

Example usage:

## Field Labels

*   Labels must appear before a form control, and must clearly identify the purpose of the control (See example above for usage)

## Input Boxes

*   Input boxes must always include placeholder text
*   Reference: [http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)  

Example usage:

## Text Areas

*   Text areas must expand the full width of the form
*   Text areas should be at least 3 rows, but no more than 7

## Checkboxes and Radio Buttons

*   If there are more that 3 checkboxes or radio buttons, the checkboxes or radio buttons should be stacked vertically
*   If there are 3 or less checkboxes and radio buttons, the checkboxes and radio buttons should appear in-line if approriate, otherwise they should be stacked vertically

## Selects

*   Default Bootstrap behavior should be used for selects

## Form Control Add-Ons

*   Form control add-ons allow for prepended and appended text to an input.
*   When add-ons are being used as button extensions, they must be appended to the end of the input. For example, when using a calendar pop-up button add-on, it must be appended to the form​. Another example, if using a search add-on, it should be appended.​​​
*   The following add-ons are recommended:

*   Currency -

*   Prepend - **$**  

*   Append - **.00**  

*   Email Address -

*   Append - **@cmich.edu**

*   URL's -

*   Prepend - **http://** or **https://**

Example usage:

## Non-Editable/Disabled Fields

*   Default Bootstrap behavior should be used for non-editable/disabled fields
*   <span><span><span>Reference: [http://getbootstrap.com/css/#forms](http://getbootstrap.com/css/#forms)</span></span></span>

## Help Text/Tooltip

*   Where appropriate, help text/tooltips should be used on form elements that may need additional explanation
*   The icon that should be used for denoting help text/tooltips is the CMich Icon**:** <span class="mls">**icon-cmich-question-6**</span>  

*   Reference: [http://getbootstrap.com/javascript/#tooltips](http://getbootstrap.com/javascript/#tooltips)

Example usage:

## Buttons

*   Primary action buttons should use the Cmich​ **Primary** button (.btn-primary-cmich)  

*   Secondary action buttons should use the Bootstrap **Default** button (.btn-default)  

*   Other button types should only be used where appropriate

*   'Add' butons - use .btn-success
*   'Delete/Remove' buttons - use .btn-warning

*   When multiple buttons are presented next to each other on a form (ie. "Submit" and "Reset"), the primary action button (in this case "Submit") should appear first. Any secondary buttons should appear to the right of this button.  

*   Reference: [http://getbootstrap.com/css/#buttons](http://getbootstrap.com/css/#buttons)

Example usage:

## Alerts

*   There are 3 types of alerts that should be used with forms:

*   Error - Error alerts must appear at the top of the form, focus must be set to the alert
*   Success - Success alerts must appear at the top of the form, focus must be set to the alert
*   Information - Information alerts can appear anywhere on the form, and should always be visible. These can be used for such things as disclaimers

*   Reference: [http://getbootstrap.com/components/#alerts](http://getbootstrap.com/components/#alerts)

Example usage:

## Required Fields

*   If a form has a mix of required and optional fields, required fields should be denoted with an asterisk (*) in their label

*   Additionally, if some or all fields are required, an alert should be added to the top of the form

## Validation Labels

*   Bootstrap **Warning** labels should be used for failed validation on form fields
*   Reference: [http://getbootstrap.com/components/#labels](http://getbootstrap.com/components/#labels)

## Tags
[[WebDesign]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=WebDesignTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
