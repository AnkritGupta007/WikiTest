# Introduction to JavaScript
In this tutorial, you will be learning how to execute and debug JavaScript.

## Outcome(s )
* Gain knowledge about JavaScript and jQuery
* Write JS in the developer console of browser dev tools and interact with various HTML elements and attributes.
* Debug JS from an externally linked JS file.

## Resource(s)
* JavaScript Tutorial - https://www.w3schools.com/js/default.asp - Please skim over everything in the "JS tutorial" section of the left navigation pane(there's a lot there). Then check out the "JS vs jQuery" and whatever "JS examples" you find interesting.
* Take the JavaScript Quiz - http://www.w3schools.com/js/js_quiz.asp - Take the quiz as many times as you need. Feel free to refer to the provided resources for help.

## Key points all developers must know:
* CSS Selectors - Selectors are the key to targeting the elements you want to bend to your will. jQuery made this easy and was the inspiration for the document.querySelectorAll() method.
* Timeouts and Intervals - These can be super helpful, but also easily abused. Always assign them to a variable so that you can clear them!
* Loops - For loops are super useful for arrays (Arrays also have a built in forEach method). For/in are great for Objects.
* XHR(a.k.a. ajax) - This is great for avoiding page loads, especially in single page applications.
* Try/Catch blocks - While error handling is definitely a good thing these can also tend to be abused. Try/catch blocks trigger error events, and error events need to dig up the stack trace to provide it for debugging. There are other, lighter weight error handling strategies, which brings us to...
* "undefined" - Nothing brings more web pages to their ruin than undefined variables. It's often good to use if(typeof(someVar) !== "undefined"){//do stuff} as opposed to abusing try/catch blocks if you can't trust what you'll be getting for data in Ajax requests. It's a good idea to initialize all variables to the data type you plan to use them for.
* Page load event - *window.onload* and *document.onload* are great events to use to attach event handlers to elements. However, resist the urge to use them to set focus on text inputs like username/password fields. Screen reader users would likely have to backtrack to see the rest of the navigation. Instead, use the *autofocus* attribute on the input. Screen readers know to ignore this.
* Event handling - how often do people enter their user name and/or password and hit enter, only to find that they have to click on an OK or submit button. The answer is "too often"! On the opposite side of that coin, how many times have you hit enter on a user name input thinking it would automagically place the cursor in the password input and have it submit the page and throw errors? Learn to handle keyboard events for each input and you'll make better forms. Also, implementing a handler for the escape key is often overlooked.

## Assignment
- To-Dos coming soon:
- Create a toggle that switches CSS files from the previous assignments.
- Replace text in whatever.
- Add, remove, and move elements
- Create a setInterval that increments colors of something.
- Create a setTimeout that makes a graphic fall from top to bottom of screen, smushing against the bottom
- Create event handlers for the keyboard to move something around the screen with arrow keys.
- Think of more To-Dos :)
 
**Submit your assignment to your Team Lead**

## Training Navigator
[<--- Zen Garden](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/-/wikis/Training-Assignment-3---CSS-Zen-Garden) ____________________________________________________________________________________________________________________ [JavaScript Bouncy Ball --->](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/-/wikis/Training-Assignment-5---JavaScript-Bouncy-Ball)

## Tags
[[JavaScript]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=JavaScriptTag)
[[Training]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TrainingTag)