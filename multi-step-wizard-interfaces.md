## When should a multi-step wizard interface be used?  

*   If a form can be broken down into several logical groupings (or steps), then a Wizard Interface should be created.

## Layout

When laying out a multi-step wizard interface, follow these guidelines:

*   This interface should take the form of multiple pages, whereby:

*   A user cannot navigate to the next page until the required fields of the current page have been completed
*   A user can navigate backwards (by one page at a time) to review/change previously entered data.
*   The final page **must** be a confirmation screen, whereby a user can jump to any of the steps to modify content if needed (this is the only time a user is allowed to jump directly to a specific section of the wizard without clicking the "Previous" or "Next" buttons).​ Once the user jumps to that page, they will have to click the "Next" button to navigate their way back to the summary.  They will not be able to jump back to the summary. This is to ensure any data that is changed is consistent in the proceeeding steps based on prior action.

### Page Title

*   The ```<H1>``` (page title) should remain consistent across pages. Often this will be the name of the application.

### Wizard Container

*   The form elements that make up the wizard interface should be housed within a Bootstrap panel with both a header and footer element.

```xml
&lt;div class=&quot;panel panel-default&quot;&gt;
	&lt;div class=&quot;panel-heading&quot;&gt;
		&lt;h2 class=&quot;margin0&quot;&gt;Step 1: Contact Information&lt;/h2&gt;
	&lt;/div&gt;
	&lt;div class=&quot;panel-body&quot;&gt;
		Form elements here...
	&lt;/div&gt;
	&lt;div class=&quot;panel-footer&quot;&gt;
		&lt;button class=&quot;btn btn-default&quot;&gt;Previous&lt;/button&gt;
		&lt;button disabled=&quot;disabled&quot; class=&quot;btn btn-primary&quot;&gt;Next&lt;/button&gt;
	&lt;/div&gt;
&lt;/div&gt;
```

#### Panel Header

*   <span style="line-height: 1.6; display: inline;">​​The panel header (```<h2>```) **must** include the step number and a label for the information being collected (ie. "Step 1: Contact Information"). This element **must** always have the "margin0" CSS class for styling purposes.</span>  

*   <span style="line-height: 1.6; display: inline;">If the number of steps in the wizard is known, the header must state the current step / the total number of steps. (ie. "Step 1 / 3: Contact Information").</span>

#### Panel Body

*   ​All relevant form elements for this step should be placed inside of the panel body. Please refer to the [[Forms]] page for proper layout of form elements.  

#### Panel Footer

<div>

*   <span style="line-height: 22.4px;">The buttons used to navigate the wizard should be placed in the panel footer. These buttons include: "Previous" and "Next".</span>

*   <span style="line-height: 22.4px;">The "Previous" button should not be visible on Step 1 of the wizard. This button should always have the "btn-default" CSS class for styling purposes as this is the secondary action.</span>
*   <span style="line-height: 22.4px;">The "Next" button should always be disabled until the required fields have been filled out for that step of the wizard. This button should always have the "btn-primary-cmich" CSS class for styling purposes as this is the primary action.  
    </span>

</div>