# Introduction to HTML
In this tutorial, you will be learning the markup language for creating web pages, HTML (HyperText Markup Language), and applying that knowledge to create a basic webpage.

## Outcome(s)
* Gain knowledge about HTML
* Create a basic HTML page

## Resource(s)
* HTML5 Tutorial - http://www.w3schools.com/html/default.asp - Please read all pages listed under 'HTML Basic' in the left column of the site.
* Take the HTML Quiz - http://www.w3schools.com/html/html_quiz.asp - Take the quiz as many times as you need. Feel free to refer to the provided resources for help.

## Key points all developers should know:
* The DOCTYPE declaration at the top of the page source code is mandatory and should not have any spaces before it.
* There should never be more than one of any of the following tags/elements: HTML, HEAD, TITLE, BODY, HEADER, MAIN, and FOOTER.
While this may seem obvious, be careful not to generate duplicates from server-side code or JS! Also, the first four elements listed above are mandatory.
* IDs must be unique - No two elements with the same ID attribute can exist in a web page or bad things will happen. If you need to act on the multiple elements with your CSS or JS code, use **classes**
* Heading levels should never be skipped. In other words, don't use an H3 tag for example, unless there are H1 and H2 tags before it.

## Assignment
Disclaimer: this will be styled in the first assignment for CSS. Until then, it will look like a big block of jibberish with a title, and that's ok.

Using the text editor of your choice (notepad++, notepad, Visual Studio, Atom, whatever you want), create a valid HTML page with the following elements:

Add a doctype of \<!DOCTYPE html\>.

Add \<meta charset="UTF-8"\> as the first thing in the 'head' element.

Set the 'title' elements text to "Assignment 1: Basic HTML".

Next add a 'Header' element inside of the "body" tag. Note that we can only have 1 header on a page, so no class or ID attribute is necessary for JS/CSS selection.

Inside of your header element, add an H1 element containing the text "Awesome Website Title" with an ID of "websiteTitle". 

After the header element, add a div with a class of "container" containing the following div's.

Inside of the "container" div, add another div with a class of "container-inner" containing the following two elements:

- a div with a class of "leftPanel". Add 3 paragraphs of text. (Generate the text using the Lorem Ipsum generator: http://www.lipsum.com/)

- a div with a class of "rightPanel". Add 1 paragraph of text. (Generate the text using the Lorem Ipsum generator: http://www.lipsum.com/)

Last, create a 'Footer' element after your "container" div. Like the header, no class or ID is necessary since you can only have one footer. Add 1 paragraph of text. (Generate the text using the Lorem Ipsum generator: http://www.lipsum.com/)

Validate the HTML - http://validator.w3.org/. Fix all errors and warnings (normally warnings aren't a big deal, but you'll probably only need to add lang="en" to your HTML tag if you wrote this entire thing from scratch).

**Submit your assignment to your [Mentor](Student-Mentoring-Pairs) & Team Lead**

## Training Navigator

[<--- Wiki Home](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/-/wikis/student-developer-training) ___________________________________________ [Intro To CSS --->](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/-/wikis/Training-Assignment-2---Intro-To-CSS)

## Tags
[[HTML]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=HTMLTag)
[[Training]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TrainingTag)