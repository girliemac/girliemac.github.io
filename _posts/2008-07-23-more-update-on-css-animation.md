---
title: More Update on CSS Animation
author: Tomomi Imura
layout: post
permalink: /blog/2008/07/23/more-update-on-css-animation/
categories:
  - CSS
  - Dev
  - iPhone
  - Sandbox
  - WebKit
---
OK, so now I am trying to clarify how to make the css animation works using class name swap.

The conclusion is that it does work! &#8211; but you need to apply the `-webkit-transition` to &#8220;destination&#8221; class not the &#8220;origin&#8221; as I first attempted. Thanks for Dave and Dean from Apple, who pointed it out.

<a href="http://girliemac.com/iphone/anim2.html" target="_blank">Go to The Actual Example Page</a>

HTML Markup used for these examles (from Apple&#8217;s doc):

```html
<div class="box" 
	style="width:100px; 
	height:100px; 
	background-color:blue;" 
	onclick="this.className = 'boxFade'"> 
Tap to fade 
</div>				
```

### What \*Not\* To Do

This worked on some older WebKit nightly builds, but not on the latest build.

The reason is the `-webkit-transition` properties into the newClassName definition.

```css
/* *** This is a bad example *** */

div.box { /* this applies only to the 'before' transition state */
-webkit-transition-property: opacity; 
-webkit-transition-duration: 2s; 
} 
div.boxFade { 
opacity:0; 
}				
```

Click the box. On clicking event, the box&#8217;s opacity turns 0 immediately because the transition properties are not set for the &#8220;after&#8221; state.

## What To Do &#8211; 1

This is the actual example snippet from Apple&#8217;s documentation, *Safari CSS Animation Guide for iPhone OS* page 13-14.  
The reason this example works is that the `-webkit-transition` properties are defined in a generic `<div>` tag, not in a specified class that applied only for &#8220;before&#8221; state.

```css
div { /* this applies for both 'before' and 'after' states */
	-webkit-transition-property: opacity; 
	-webkit-transition-duration: 2s; 
} 
div.fadeAway { 
	opacity:0; 
}				
```

## What To Do &#8211; 2

Move all the `-webkit-transition` properties into the newClassName definition.

```css
div.fadeAway { /* give the transition rules to "after" state */
	opacity:0; 
	-webkit-transition-property: opacity; 
	-webkit-transition-duration: 2s; 
}				
```

Now really a JavaScript-free. Yay.