# Summary 
Making a border-radius style button in email, without an image, that works with outlook and web can be done, but it's a bit tricky. Below is a working example of how this can be done using html email. 

For more full context on how this is used, you can look for `ADApprovalRequest` in `CMich.FMServiceRequest` such as in this spot in the [HomeController.cs](https://code.cmich.edu/App-Custom/CMich.FMServiceRequest/blob/master/CMich.FMServiceRequest/Controllers/HomeController.cs#L771).

```xml
<!DOCTYPE html PUBLIC '-//W3C//DTD HTML 4.01//EN' 'http://www.w3.org/TR/html4/strict.dtd'><html><head>
<meta http-equiv="Content-Type" content="text/html; charset=us-ascii"> <title>Work Order Request Receipt</title>
<style type="text/css">
body {
	padding: 0; margin: 0; color: #333; background: #fff; font: normal 76%/1 'Lucida Grande', Helvetica, 'Trebuchet MS', sans-serif; font-size: 14px; text-align: center;
}
a {color: #6A0032; text-decoration: none;}'
a:hover {text-decoration: underline;}
table.table-data {text-align:left;}
.button-link {
	background-color:#6A0032;
	border:1px solid #6A0032;
	border-radius:3px;
	color:#FFF;
	display:inline-block;
	font-family:sans-serif;
	font-size:16px;
	line-height:44px;
	text-align:center;
	text-decoration:none;
	width:150px;
	-webkit-text-size-adjust:none;
	mso-hide:all;
}
.outlook-button {
	color:#FFF;
	font-family:Helvetica, Arial,sans-serif;
	font-size:16px;
}

</style>
</head><body><center>
<strong>As the account director, you must <em>approve</em>  or <em> deny</em>  this request.</strong> 
<br>
<br>Please click this button to do so:
<!-- our border-radius button --> 
<table width="100%" border="0" cellspacing="0" cellpadding="0">
  <tr>
    <td valign="middle" align="center">
      <div>
	    <!--[if mso]>
          <v:roundrect xmlns:v="urn:schemas-microsoft-com:vml" xmlns:w="urn:schemas-microsoft-com:office:word" href="{Link}" style="height:36px;v-text-anchor:middle;width:150px;" arcsize="5%" strokecolor="#6A0032" fillcolor="#6A0032">
            <w:anchorlock/>
            <center class="outlook-button">Manage Approval</center>
          </v:roundrect>
		<![endif]-->
        <a href="{Link}" class="button-link">Manage Approval</a>
      </div>
    </td>
  </tr>
</table>
</center></body></html>
```

## Tags
[[Email]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=EmailTag)
[[CSS]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSSTag)
[[HTML]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=HTMLTag)