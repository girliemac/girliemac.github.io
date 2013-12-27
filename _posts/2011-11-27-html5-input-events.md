---
title: HTML5 Input Event Handlers and User-Experience
author: Tomomi Imura
layout: post
permalink: /blog/2011/11/27/html5-input-events/
topsy_short_url:
  - http://is.gd/5MCIYH
  - http://is.gd/5MCIYH
dsq_thread_id:
  - 2067859906
categories:
  - HTML5
  - JavaScript
  - UI/UX
---
## TL;DR

Summary: Use `oninput` event handler (or `input` event handler event type) when you register an event to the HTML5 `input[type="number"]`, instead of `onchange`, `onkeyup/down` (although you may want to include them as the fall-back).

## The Whole Story

When I participated to compete for <a href="http://nodeknockout.com/" target="_blank">Node.js Knock-out</a> in the end of the summer, I have learned one thing (besides all the node.js coolness) in a bitter way, from the comments by judges: &#8220;the app UI is confusing.&#8221;  
Actually, I believed that the app user-interface overall was intuitive enough, however, the one mistake I made with an HTML5 form killed the user-experience &#8211; I used a wrong event handler, something that doesn&#8217;t trigger when it needed to&#8230; 

So here, I explain what I didn&#8217;t know; the newly introduced event handlers for HTML5.

<img src="/assets/images/wp-content/uploads/2011/11/input-number.png" alt="input type=number" title="input-number" width="221" height="117" />

The screenshot above is a number input control, the input element with a type attribute which value is &#8220;number&#8221;. It represents a precise control for setting the element&#8217;s value to a string representing a number.

Simply, you can write this in html like this:

```html
<input type="number" placeholder="Pick a number" id="numPeople" />
```

You can add some more custom attributes like, `required`, `autofocus`, `pattern`, etc, and the number-specific attributes, `min`, `max`, and `step`. If you are not familiar with the html5 form input attributes, I recommend you should read <a href="http://dev.opera.com/articles/view/new-form-features-in-html5/" target="_blank">New form features in HTML5</a> by Dev Opera.

So what I wanted to do in the particular app was that populating new fields as the user chooses a number. The simple user-flow is:  
  
1. &#8220;How many people would you like to add?&#8221; &#8211; e.g. a user picks 5  
2. n-number of new fileds are populated &#8211; e.g. 5 text fileds are displayed  
3. the user fills out the text fields  
4. the user submit the form 

<img src="/assets/images/wp-content/uploads/2011/11/input-number2.png" alt="screenshot" title="input-number2" width="340" height="300" class="alignnone size-full wp-image-338" />

To make the flow #1 and #2 work, what I did was that I registered an event listener to the number input element, and used an event type to listen for.  
OK, so which event type? &#8211; Well, I initially thought of `change`, however, it requires the user to unfocus (blur) the field once, to get the event captured. So, I decided to use `keyup` so as soon as the user finish typing a number, the event is fired and the function to display the extra fields is called.

OK, it sounds fine &#8211; well, only as long as the user only enter the number manually! 

Remember, the HTML5 input field `type="number"` has the special user-interface, *a spinner control*, which allows a user to increment and decrement its value. And here is the problem &#8211; the *keyup* event does *not* get triggered when the spinner up/down arrow is clicked, at least on Chrome (which the judges were using)! So when some judges tried the app for the first time without much knowing what it does, and picked a number with the spinner control, nothing happened. The app&#8217;s UX was killed right there!

So, really, which event did I need to use? 

The answer is `input`. I did not know about the newly introduced HTML5 `oninput` event handler until I found <a href="http://whattheheadsaid.com/2010/09/effectively-detecting-user-input-in-javascript" target="_blank" />this article</a>.

Now, the action is triggered when a user manually type a number, or when the user increment/decrement with the up/down spinner!

```javascript
var numPeople = document.getElementById("numPeople");

numPeople.addEventListener("input", function(e) {
    var num = numPeople.value;
    ...
}, false);
```

Please see the entire <a href="http://jsfiddle.net/girlie\_mac/CcqU7/" target=\_blank">code snippet and working demo</a>!

Also, I made <a href="http://jsfiddle.net/girlie\_mac/5Assc/" target=\_blank">another small demo here</a> so you can see when the `input`, `keuyp`, and `change` are captured.

## onsearch Event

Additionally, there is another HTML5 event that you probably want to know &#8211; the `search`. The action is invoked when a user hits the enter key or clears the query (by clicking the (x) in a search control.  
I can&#8217;t find any references in WHATWG or W3C, and apparently, its upport Level is the Apple extension. I tested it work on the latest Chrome, but not on Firefox 9 or Opera 11.5.

<img src="/assets/images/wp-content/uploads/2011/11/input-search.png" alt="input[type=search]" title="input-search" width="250" height="115" class="alignnone size-full wp-image-347" />

```html
<input type="search" name="username" placeholder="Enter a Twitter username..." results="5" id="search" />
```

```javascript
var s = document.getElementById("search");
s.addEventListener("search", function(e) {
    var q = s.value;
    showTweets(q);
}, false);
...
```

The <a href="http://jsfiddle.net/girlie\_mac/sfxYG/" target=\_blank">code snippet and demo</a> is at jsFiddle, too!

## References

<a href="http://www.whatwg.org/specs/web-forms/current-work/" target=_blank">whatwg.org &#8211; Web Forms 2.0</a>  
<a href="http://www.whatwg.org/specs/web-apps/current-work/multipage/webappapis.html#handler-oninput" target=_blank">whatwg.org &#8211; oninput Event Handler</a>  
<a href="http://whattheheadsaid.com/2010/09/effectively-detecting-user-input-in-javascript" target=_blank">Effectively detecting user input in JavaScript</a>  
<a href="http://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariHTMLRef/Articles/Attributes.html#//apple\_ref/html/attribute/onsearc" target=\_blank">Safari HTML Reference (onsearch)</a>