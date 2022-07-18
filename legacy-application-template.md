<div class="alert alert-info">The following guidelines should be followed for all new custom applications that don't have their own unique branding. Any exceptions must be discussed with Jesse.</div>

<span style="line-height: 1.6;">To</span> <span style="line-height: 1.6;">maintain a coherent look and feel between applications, and to create a unified experience for users, an Application Template has been created to serve these needs. **The Application Template must be used for ALL new custom applications being developed.**</span>  

2 versions of the Application Template have been developed, a pure HTML version and an MVC application. These can be downloaded from vault at:

*   $\Designs\applicationTemplateBootstrap3
*   $\Designs\CMich.ApplcationTemplateBootstrap3MVC

A "Demo" site has also been setup on the CDN at: [http://cdn.cmich.edu/css/applicationTemplate/demo/applicationTemplate.html](http://cdn.cmich.edu/css/applicationTemplate/demo/applicationTemplate.html) . This demo site shows the many different options and layouts that can be accomplished with the different pieces of the Application Template.

For documentation on how the application template is intended to be used and <span>application template specific code snippets</span>, please refer to:

[http://cdn.cmich.edu/css/applicationTemplate/demo/applicationTemplateSnippet.html](http://cdn.cmich.edu/css/applicationTemplate/demo/applicationTemplateSnippet.html)

## Helper Classes

The following is a list of classes to be used to quickly apply styles to DOM elements. (Applies to version 1.1.0+ of the Application Template stylesheet)  

<span class="ms-rteThemeForeColor-5-4">Positioning Classes</span>

The following classes are for positioning elements within a page. The asterisk(*) denotes a variable that needs to be replaced with 0, 5, 10, 15, 20, 25, or 30 to specify the pixel dimension of the desired class. So, for example, to add a margin of 15 px to all sides of an element, use the class <span class="ms-rteFontFace-10">margin15</span>. If you want to remove a margin or padding, use 0 as the variable. So, for example, if you want to remove the bottom padding of an element, add the class <span class="ms-rteFontFace-10">paddingBottom0</span> to the element.  

<table cellspacing="0" class="ms-rteTable-default" style="width: 45%;">

<tbody>

<tr class="ms-rteTableEvenRow-default" style="text-align: center;">

<td class="ms-rteTableEvenCol-default" style="width: 50%;"><strong>CLASS NAME</strong> 
</td>

<td class="ms-rteTableOddCol-default" style="width: 50%;"><strong>CLASS DESCRIPTION</strong></td>

</tr>

<tr class="ms-rteTableOddRow-default">

<td class="ms-rteTableEvenCol-default">margin*****</td>

<td class="ms-rteTableOddCol-default" style="text-align: center;">Targets margin to all sides of the element  
</td>

</tr>

<tr class="ms-rteTableEvenRow-default">

<td class="ms-rteTableEvenCol-default">marginTop*****</td>

<td class="ms-rteTableOddCol-default" style="text-align: center;">Targets margin on the top of the element only  
</td>

</tr>

<tr class="ms-rteTableOddRow-default">

<td class="ms-rteTableEvenCol-default">marginBottom*****  
</td>

<td class="ms-rteTableOddCol-default" style="text-align: center;">​<span>Targets margin on the bottom of the element only</span></td>

</tr>

<tr class="ms-rteTableEvenRow-default">

<td class="ms-rteTableEvenCol-default">marginLeft*****</td>

<td class="ms-rteTableOddCol-default" style="text-align: center;">​<span>Targets margin to the left of the element only</span></td>

</tr>

<tr class="ms-rteTableOddRow-default">

<td class="ms-rteTableEvenCol-default">marginRight*****</td>

<td class="ms-rteTableOddCol-default" style="text-align: center;">​<span>Targets margin to the right of the element only</span></td>

</tr>

<tr class="ms-rteTableEvenRow-default">

<td class="ms-rteTableEvenCol-default">​</td>

<td class="ms-rteTableOddCol-default">​</td>

</tr>

<tr class="ms-rteTableOddRow-default">

<td class="ms-rteTableEvenCol-default">padding*</td>

<td class="ms-rteTableOddCol-default" style="text-align: center;">Targets padding on all sides of the element  
</td>

</tr>

<tr class="ms-rteTableEvenRow-default">

<td class="ms-rteTableEvenCol-default">paddingTop*</td>

<td class="ms-rteTableOddCol-default" style="text-align: center;">Targets padding on the top of the element only  
</td>

</tr>

<tr class="ms-rteTableOddRow-default">

<td class="ms-rteTableEvenCol-default">paddingBottom*</td>

<td class="ms-rteTableOddCol-default" style="text-align: center;">Targets padding on the bottom of the element only  
</td>

</tr>

<tr class="ms-rteTableEvenRow-default">

<td class="ms-rteTableEvenCol-default" rowspan="1">paddingLeft*</td>

<td class="ms-rteTableOddCol-default" rowspan="1" style="text-align: center;">Targets padding to the left of the element only  
</td>

</tr>

<tr class="ms-rteTableOddRow-default">

<td class="ms-rteTableEvenCol-default" rowspan="1"><span class="ms-rteThemeForeColor-2-0">paddingRight*</span></td>

<td class="ms-rteTableOddCol-default" rowspan="1" style="text-align: center;">​<span class="ms-rteThemeForeColor-2-0">Target padding to the right of the elemeny only</span>  
</td>

</tr>

<tr class="ms-rteTableEvenRow-default">

<td class="ms-rteTableEvenCol-default" rowspan="1">​​</td>

<td class="ms-rteTableOddCol-default" rowspan="1" style="text-align: center;">​</td>

</tr>

<tr class="ms-rteTableFooterRow-default">

<td class="ms-rteTableFooterEvenCol-default" rowspan="1"><span class="ms-rteThemeForeColor-2-0">table- no-overflow</span></td>

<td class="ms-rteTableFooterOddCol-default" rowspan="1" style="text-align: center;"><span class="ms-rteThemeForeColor-2-0">Fixes the horizontal scroll bar with Data-Tables</span></td>

</tr>

</tbody>

</table>

## Buttons

There should only be **ONE** btn-primary-cmich per action area.  

When using a button that designates a primary action, use the btn-primary-cmich class **NOT** the bootstrap btn-primary class. We are overwriting the primary Bootstrap blue with our maroon using the .btn-primary-cmich class. 

## MVC Application Template  

The ASP.Net MVC version of the application template can be found at: [https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/](https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/)    

It includes documentation and example on the following

### Basic App template done in MVC

- [https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/](https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/)    

### Email Form template

- [https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/EmailForm](https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/EmailForm)    

### MonthDayYear JQuery plugin template

- [https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/MonthDayYear](https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/MonthDayYear)  which is used as a date picker, or just a year and month picker, without the day.  

### Multiselect JQuery Plugin template

- [https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/Multiselect](https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/Multiselect)    

### RequiredIf JQuery Plugin template

- [https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/RequiredIf](https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/RequiredIf)    

### VisualCaptcha JQuery Plugin template

- [https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/VisualCaptcha](https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/VisualCaptcha)  

### Request Form template

- [https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/Create](https://resapps.cmich.edu/ApplicationTemplateBootstrap3MVC/Home/Create)

## Tags
[[Development]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=DevelopmentTag)
[[FrontEnd]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=FrontEndTag)
[[Template]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TemplateTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
