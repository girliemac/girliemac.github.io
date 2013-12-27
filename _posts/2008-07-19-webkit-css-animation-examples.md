---
title: WebKit CSS Animation Examples
author: Tomomi Imura
layout: post
permalink: /blog/2008/07/19/webkit-css-animation-examples/
categories:
  - CSS
  - Dev
  - iPhone
  - Sandbox
  - WebKit
---
According to <a href="http://webkit.org/blog/138/css-animation/" target="_blank">WebKit.org</a>, the WebKit supports the simplest kind of animation called a *transition*.

Transitions are specified using the following properties:

*   **transition-property** &#8211; What property should animate, e.g., opacity.
*   **transition-duration** &#8211; How long the transition should last.
*   **transition-timing-function** &#8211; The timing function for the transition (e.g., linear vs. ease-in vs. a custom cubic bezier function).
*   **transition** &#8211; A shorthand for all three properties.

Last week, I&#8217;ve noticed that Apple had published some new documentations at <a href="https://developer.apple.com" target="_blank">Developer Connection</a>, including  
*Safari CSS Animation Guide for iPhone OS* and *Safari CSS Transforms Guide for iPhone OS* (Go to <a href="https://developer.apple.com/webapps/docs_iphone/referencelibrary/index-date.html" target="_blank">download page</a>).  
Since I read the WebKit.org blog entry last year, I was interested in the CSS animation so I finally decided to give it try. 

I spent some time writing several CSS tests, ran on several different WebKit browsers. and my conclusion is that:

1.  the animation and transforms are pretty buggy on current iPhone Safari. 
2.  the current WebKit nightly (as of July 19) has some bugs so animation doesn&#8217;t work when swapping class names 
with oncick event handler attributes like, using `this.className='newClassName'`. </ol> 
The className swap was working perfectly, until I installed the newer build, r35231.  
I will file the bug to Webit.org soon.   
  
On latest build, build r35075 &#8211; r35231 (the newest one I tested),  
changing the values of `style` object properties, instead, as  
`onclick="this.style.opacity='0'"`  
  
I wanted to create the animation entirely absent of JavaScript, but now I need to use a function to handle multiple style properties&#8230; 

<a style="color:red; font-weight:bold; font-size:105%;" href="/blog/2008/07/23/more-update-on-css-animation/"><br /> UPDATE / CORRECTION (July 23, 08) &#8211; please see &#8220;More Update on CSS Animation&#8221;</a>

I still haven&#8217;t gotten a chance to try iPhone 3G yet, and I tested only on my old iPhone with the latest upgrade.  
Are there any differences in between two Safaris? I doubt it.

Anyway, <a href="/iphone/anim.html" target="_blank">Open the test page</a> I wrote in a new window!

## Animate Opacity

<a href="/iphone/anim.html#opacity" target="_blank">Opacity Transition Test</a>

Expected result: When a user mouse-overs the box, an object appears smoothly (opacity=.5) in 2 sec.  
On mouse-click, the image fades in completely (opacity=1). 

```css
.box1 img{
	opacity: 0;
	-webkit-transition: opacity 2s ease-out;   /* shorthand for all three properties */
}
.box1 img:hover {
	opacity: .8;
}
```

```html
<div class="box1">
	<img src="images/apple.png"/>
</div>
```

## Animate Position &#8211; Move to right

<a href="/iphone/anim.html#position" target="_blank">Position Transition Test</a>

Expected result: the image moves to the right as fading out.

```css
.box2{
	opacity: 1;
  	-webkit-transition-property: opacity, left;
	-webkit-transition-duration: 1s, 1.5s;
	transition-timing-function: ease-in;
}			
```

```html
<div class="box2" onclick="this.style.opacity='0'; this.style.position='relative'; this.style.left='500px'">
	<img src="images/apple.png"/>
</div>
```

## Animate Letters &#8211; Letter-Spacing

<a href="/iphone/anim.html#letters" target="_blank">Letter-Spacing Test</a>

Expected result: When the text is clicked, each letter spaces out as fading away.

It is pretty cumbersome to handle multiple style properties with onclick, so I added a JavaScript function to take care:

```javascript
function switchStyles(style,obj) {
	for(var prop in obj)
		style[prop] = obj[prop];
}
```

<a style="color:red; font-weight:bold; font-size:105%;" href="/blog/2008/07/23/more-update-on-css-animation/"><br /> UPDATE / CORRECTION (July 23, 08) &#8211; You don&#8217;t need this hassle with JS. Please see &#8220;More Update on CSS Animation&#8221;</a>

```css
.box3{
	color: green;
	opacity: 1;
  	-webkit-transition-property: opacity, letter-spacing;
	-webkit-transition-duration: 1.5s, 2s;
	transition-timing-function: ease-out, linear;
}			
```

```html
<div class="box3" 
     onclick="switchStyles(this.style,{
	    color : 'lime',
	    opacity : '0',
	    letterSpacing : '3em'
});">
	some text to be clicked here.
</div>			
```

## Transform &#8211; Click to spin the image and fade away

<a href="/iphone/anim.html#transform" target="_blank">Position Transition Test</a>

Expected result: the image rotates twice (360 deg x 2) around the Z axis, as fading.

```css
.box4{
  	-webkit-transition-property: -webkit-transform, opacity;
	-webkit-transition-duration: 2s;
	transition-timing-function: cubic-bezier(0.42, 0, 0.58, 1.0); /* equivalent to ease-in-out */
}				
```

```html
<div class="box4" 
	 onclick="switchStyles(this.style,{
	    webkitTransform: 'rotate(720deg) translate(1000px,0px)',
		opacity: '0'
});">
	<img src="images/apple.png"/>
</div>				
```

Also, I tried CSS gradients. These still don&#8217;t seem to work on iPhone but worked on all recent WebKit nightly.

## CSS Gradients &#8211; Linear and Radial

<a href="/iphone/anim.html#gradient" target="_blank">Gradients Test</a>

Expected results:  
Linear &#8211; Green to white top-to-bottom linear gradient  
Radial &#8211; White to pink center-to-outer radial gradient  
Actual results:  
Nicely working on WbKit nightly builds. Failed miserably on both Mac desktop and iPhone Safari 3.1. 

Screenshot of the results on WebKit nightly  
![][1]  
  
The syntax is as follows:  
`-webkit-gradient(<type>, <point> [, <radius>]?, <point> [, <radius>]? [, <stop>]*)` 

```css
#gradientLinear{
	float: left;
	width: 180px;
	height: 180px;
	border: 1px solid #11276c;
	background:	
		-webkit-gradient(linear, left top, left bottom, from(rgba(158,192,0,.85)), color-stop(1, #fff));
}

#gradientRadial{
	float: left;
	margin-left: .5em;
	width: 180px;
	height: 180px;
	border: 1px solid #11276c;
	background:	
		-webkit-gradient(radial, center center, 3, 80 80, 100, from(rgb(255,255,255)), to(rgba(228,56,132,.85)), color-stop(0%,#fff));
}				
```


### Resources:

1.  <a href="http://webkit.org/blog/138/css-animation/" target="_blank">Surfin&#8217; Safari &#8211; CSS Animation</a>
2.  <a href="http://webkit.org/blog/175/introducing-css-gradients/" target="_blank">Surfin&#8217; Safari &#8211; Introducing CSS Gradients</a>
3.  <a href="https://developer.apple.com/webapps/docs_iphone/documentation/iPhone/Conceptual/SafariCSSAnimationGuide/Introduction/chapter_2_section_1.html" target="_blank">Safari CSS Animation Guide for iPhone OS</a>
4.  <a href="https://developer.apple.com/webapps/docs_iphone/documentation/iPhone/Conceptual/SafariCSSTransformGuide/Introduction/chapter_2_section_1.html#//apple_ref/doc/uid/TP40007134-CH1-SW1" target="_blank">Safari CSS Transform Guide for iPhone OS</a>

 [1]: /assets/images/wp-content/misc/gradients.png