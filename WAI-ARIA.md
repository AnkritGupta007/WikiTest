## ​​​​What is WAI-ARIA?

​WAI-ARIA (Web Accessibility Initiative - Accessible Rich Internet Application) <span style="line-height: 1.42857;">defines a way to make Web content and Web a</span><span style="line-height: 1.42857;">pplications more accessible to people with disabilities. It especially helps with dynamic content and advanced user interface controls developed with Ajax, HTML, JavaScript, and related technologie</span>

<div>In addition to user interaction controls, ARIA provides ways to better enable use of web pages as a whole. “Landmark roles” allow authors to annotate regions of the page so users can find them quickly; this is important when users don’t have the overall knowledge of the page layout often represented in graphical browsers. Navigation and search regions, ancillary content, and of course the main content can be marked so users can find the region they need at the moment. The technology also allows authors to indicate content that should be treated more like a software application than as document content, so assistive technologies can provide application-specific behavior. Finally it provides ways to handle regions of the page that automatically update their content, such as stock tickers or chat applications, which can be disruptive or unpercievable to some assistive technology users without the mediation provided by ARIA.​</div>

## Rules of ARIA

### First Rule of ARIA

If you can use a native HTML element [HTML51] or attribute with the semantics and behaviour you require already built in, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, then do so.

<span style="line-height: 1.42857;">​Under what circumstances may this not be possible:</span>

1.  <span style="line-height: 1.42857;">If the feature is available in HTML [HTML51] but it is not implemented or it is implemented, but accessibility support is not.</span>
2.  <span style="line-height: 1.42857;">If the visual design constraints rule out the use of a particular native element, because the element cannot be styled as required.</span>
3.  <span style="line-height: 1.42857;">If the feature is not currently available in HTML.</span>  

### Second Rule of ARIA

<div>Do not change native semantics, unless you really have to.</div>

<div>For example: Developer wants to build a heading that's a button.</div>

<div>Do **NOT** do this:
</div>

```html
<h1 role=button>heading button</h1>
``` 

<span style="line-height: 1.42857;"></span>

**Do** this:

```html
<h1><button>heading button</button></h1>
```
​​Or, if you can't possible use the correct element, **do** this:  

```html
<h1><span role=button>heading button</span></h1>
```

### ​Third rule of ARIA  

<div>All interactive ARIA controls must be usable with the keyboard.</div>

<div>If you create a widget that a user can click or tap or drag or drop or slide or scroll, a user must also be able to navigate to the widget and perform an equivalent action using the keyboard.</div>

<div>All interactive widgets must be scripted to respond to standard key strokes or key stroke combinations where applicable.</div>

<div>For example, if using role=button the element must be able to receive focus and a user must be able to activate the action associated with the element using both the enter (on WIN OS) or return (MAC OS) and the space key.</div>

<div>Refer to the [keyboard and structural navigation](http://www.w3.org/WAI/PF/aria-practices/#keyboard) and [design patterns​](http://www.w3.org/WAI/PF/aria-practices/#aria_ex) sections of the [WAI-ARIA 1.0 Authoring Practices](http://www.w3.org/WAI/PF/aria-practices/)​.</div>

### Fourth rule of ARIA​

<div>Do not use role="presentation" or aria-hidden="true" on a visible focusable element .</div>

<div>Using either of these on a visible focusable element will result in some users focusing on 'nothing'.</div>

<div>Do **NOT** do this:</div>

```html
<button role=presentation>press me</button>
```
​​Do **NOT** do this:  

```html
<button aria-hidden="true">press me</button>
```
​​

### ​Fifth rule of ARIA

<div>

<div>All interactive elements must have an accessible name.</div>

<div>An interactive element only has an accessible name when it's Accessibility API accessible name (or equivalent) property has a value.</div>

<div>For example,  the input type=text in the code example below has a visible label 'user name' and an accessible name. This example has an accessible name because the input element is a labelable element and the label element is used correctly to associate the label text with the input.​:</div>

```html
<label for="uname">user name</label>
<input type="text" id="uname">
```

</div>

## Tags
[[HTML]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=HTMLTag)
[[OldWiki]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=OldWikiTag)
[[​Accessibility]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=​AccessibilityTag)