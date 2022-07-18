## Summary
​This article will describe how to get intellisense for JavaScript libraries that are hosted on our CDN.
## _refences.js  

You will need to include a file titled **_references.js** in the folder **Scripts **​at the root of your project. Every time you add a new reference to this file, close and reopen any file that you need the intellisense on. This would include views, JavaScript libraries, etc...​  

## ​​​​​References for the Application Template  

If you are using the general CMich Application Template, the following lines should be in your _references.js file. The newest version of the application template has this file included and already setup with these references.​  

~~~Javascript
/// &lt;reference path=&quot;https://cdn.cmich.edu/jquery/1.10.2/jquery-1.10.2.js&quot; /&gt; 
/// &lt;reference path=&quot;https://cdn.cmich.edu/bootstrap/3.3.2/js/bootstrap.js&quot; /&gt; 
/// &lt;reference path=&quot;https://cdn.cmich.edu/jquery/plugins/ValidateUnobtrusive/5.2.3/jquery.validate.unobtrusive.js&quot; /&gt; 
/// &lt;reference path=&quot;https://cdn.cmich.edu/js/applicationTemplate/1.0.0/applicationTemplate.js&quot; /&gt; 
~~~

## ​​​​Example of an additional library   

If you are using a different library from the CDN that is not part of the standard application template you can include it by putting the following in your _references.js file. It is recommended that you link to the non-minified version.  

~~~Javascript
/// <reference path="<URL_TO_JAVASCRIPT_FILE>" />
 
For Example the bootstrap datetime picker
 
/// <reference path="https://cdn.cmich.edu/bootstrap/plugins/datetimepicker/4.17.37/js/bootstrap-datetimepicker.js" />
~~~

## Tags
[[Javascript]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=JavascriptTag)​​
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)