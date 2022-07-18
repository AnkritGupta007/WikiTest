# The JavaScript Bouncy Ball: An exercise in DOM manipulation based animation

This exercise is meant to be a little more fun, while giving you some first hand experience at old school animation the way jQuery's "animate" function does it, but we're using totally vanilla JavaScript here. You will start with just making an HTML element that moves across the screen. As you progress, you'll add logic to make it move diagonally across the screen, bounce off the edges, and even be able to pause the animation, and eventually control it with the arrow keys! This assignment will likely have you doing web searches to figure out how to make stuff happen, and how stuff works. Note, for improved performance this could be made not-so old school implementing CSS3 transitions and variables to take advantage of hardware acceleration. 

So enough about what we're about to do. Lets get started!

### Create the HTML page
This entire thing can be done in one HTML file if you wish. Or, if you want to put your JavaScript in a separate file instead of in the end of the BODY tag, that's entirely up to you. So go ahead and make an empty HTML5 page with the usual HTML, HEAD, TITLE, and BODY tags.

### Create the Bouncy ball element.
For this, just create a DIV with an ID attribute of your choosing. For this to work, you'll need a style attribute with "top" and "left" values set to "60px" or so to start, just to make sure you're not "out of bounds" (You'll see why later). At this point, your page will still look completely blank.

### Use CSS to make our element into a visible ball
Create a style tag in the HEAD of the document. Give your DIV element a height and width in pixels, absolute positioning, a background of whatever you want, and a border radius value that is half of the height (also in pixels). At this point, you should be able to view your creation in the browser, but of course, it won't move.

### Time to start adding JavaScript. Now the real fun begins!
The heart of this will be powered by a `setInterval` function. Start with a 15 millisecond interval (hint, make the interval a variable for later). Start by just making an interval function that moves the ball across the screen, but stops at the edge. To do this, you'll need to know the width of the screen, which is accessible by the `window.innerWidth` property. The idea is that the ball's left position is incremented by a pixel or two every interval. For this, you'll need to get the current position of the ball and make sure it doesn't exceed the width of the page (minus the width of your ball if you want it to stop at the edge). With the current position known, we can compare it to the width of the screen in an `if` statement. If the `left` position is less than the screen width, increment the position. We're going to need to grab the DOM node of the ball and store it in a variable. This variable will be our "handle" moving forward. For the sake of this tutorial, I'll refer to the element as "bouncy".

But not so fast! The screen width and height are integer values. The positioning is a string like `"10px"`. To make this into something that works for our needs, it has to be an integer, so you'll need to use `parseInt(bouncy.style.left.replace("px", "")`, where `"bouncy"` represents your variable, and `style.left` is the property you are trying to get. `replace` is a method avalaible for all strings, and `style.left`'s value is always a string. We're replacing `"px"` with nothing, or effectively removing it from the string, but if you want to experiment with sub-strings, that's fine too. Once all that is done, we can use parseInt to convert what's left of the string to an integer so we can do math with it. After the `if` statement evaluates, you'll be able to increment the current `x` position and append `"px"` to typecast back to a string and assign it as the new value of `bouncy.style.left`. At this point, you should have a ball that moves to the edge of the screen, but stops shy of going off of it. Also, we have an interval function that never ends, so if that bothers you, assign the interval function to a variable so you can use the developer console to clear the interval.

### Time to make the ball bounce off the edges of the screen
If you haven't already done so, you're going to need to make your positioning increment based on an integer variable. This variable will need to be multiplied by -1 once the ball hits the edge of the screen. Just a hint, you'll use an `else` clause on your `if` statement to make this happen, and you'll want to increment the position after multiplying your increment var by -1. You'll need to update your `if` statement to have an AND (&&) clause to also check to make sure the ball hasn't returned back to the left edge of the screen. Just use `2` as your `left` side limit value.

### Add another direction
Right now we're using the `left` position style attribute to move the ball along the x axis. Copy and re-purpose the existing if/else block and variables to make it also increment the `top` position style attribute. At this point, you should have the ball bouncing off all sides of the screen.

That's it for now. The next addition to this will include changing the speeds of x/y axis travel, adding a pause button, and making a function that changes the timeout by blowing away the interval function, and creating a new one passing in the interval.

**Submit your file(s?) to your team lead.** If you have any questions or just get stumped, ask Bryan VanMeter or Eric Johnson for help.

## Training Navigator
[<--- JavaScript Basics](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/-/wikis/Training-Assignment-4---JavaScript-Basics) ___________________ [Bootstrap --->](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/-/wikis/Training-Assignment-6---Bootstrap)

## Tags
[[CSS]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=CSSTag)
[[WebDesign]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=WebDesignTag)
[[Training]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=TrainingTag)