---
title: 'Touchy-Feely with DOM Events: Rethinking Cross-Device User Interaction'
author: Tomomi Imura
layout: post
permalink: /blog/2013/04/17/touchy-feely-with-dom-events-rethinking-cross-device-user-interaction/
topsy_short_url:
  - http://is.gd/DYZ1yy
  - http://is.gd/DYZ1yy
categories:
  - HTML5
  - IE
  - JavaScript
  - Mobile
  - Nokia
  - UI/UX
  - W3C
  - WindowsPhone
---
*This article was originally written for <a href="http://www.developer.nokia.com/Blogs/Code/2013/04/02/touchy-feely-with-dom-events-rethinking-cross-device-user-interaction/" target="_blank">Nokia Code Blog</a> on the earlier this month, and I am re-posting it here with a permission.*

* * *

There have been numerous ways for users to interact with web pages on mobile phones. Historically, users navigated the mobile web by pressing physical buttons (arrow keys, soft keys, etc.), while some devices required a stylus.

In last several years, devices with touch-enabled screens have been adopted at such a rapid rate that the touch interaction has become ubiquitous. Now we have tablets that take input not only from touch, but from keyboards and mousepads using optional peripherals.

So what does it mean to you as a web developer? It means you need to detect the correct user input method, and design the correct user experience into your web apps.

In this article, I will explain the state of touch APIs in terms of current web standards, and show you some sample code to demonstrate.

![demo on Lumia](/assets/images/articles/2013/04/touch-lumia920.jpg "Touch demo on Lumia 920")

## Touch Events V.1

The touch interface was widely popularized when Apple&#8217;s iPhone came out, and the DOM touch event was also defined and implemented first on iOS Safari by Apple. Since then, it has been adopted by other browser vendors like Google and Mozilla, as well as web developers as the *de-facto* standard.

W3C defined the <a href="http://www.w3.org/TR/touch-events/" target="_blank">touch events specification</a> as a set of low-level events that represent one or more points of contact with a touch-sensitive surface, as well as changes to those points with respect to the surface and any DOM elements displayed on or associated with it.

The event types include: `touchstart`, `touchend`, `touchmove`, `touchenter`, `touchleave` and `touchcancel`.

![Touch events](/assets/images/articles/2013/04/touchevents.png "Touch events")

### Example

The following code snippet, used in <a href="https://dl.dropbox.com/u/1330446/demo/touch-events.html" target="_blank">this example demo</a>, determines the position (in pixel coordinates) of a finger within a canvas element when a touch action is initiated by the user.

The demo tracks a user&#8217;s touch points, allowing the user to draw on a kitty cat (in `<canvas>`). It will only work on browsers that supports touch events on touch-enabled devices. If you are trying it on a desktop using a mouse or trackpad, you&#8217;ll notice that nothing happens on screen.

```javascript
var canvas = document.getElementById('drawCanvas');

canvas.addEventListener('touchstart', function(e) {
e.preventDefault(); // canceling default behavior such as scrolling
var x = e.targetTouches[0].pageX - canvas.offsetLeft;
var y = e.targetTouches[0].pageY - canvas.offsetTop;
}, false);
```


## U Can&#8217;t Touch This

So how do you make it work on the desktop when touch events do not fire with a non-touch user input? To support mouse or trackpad events, you need to use the DOM `MouseEvents`.

```javascript
canvas.addEventListener('mousedown', function(e) {
var x = e.offsetX || e.layerX - canvas.offsetLeft; 
var y = e.offsetY || e.layerY - canvas.offsetTop;
}, false);
```


So I wrote <a href="https://dl.dropbox.com/u/1330446/demo/mouse-events.html" target="_blank">another demo</a> to demonstrate this.

This demo uses mouse events instead of the touch events, but not both types of events. Try it on a desktop browser and see how it works, and then see how it fails on touch-enabled devices.

To make both user input methods work, you need to support both touch and mouse events together.  
When using `touchstart`, `touchmove`, and `touchend`, you also need to implement using `mousedown`, `mousemove` and `mouseup` respectively.

The completed demo is at the end of this article.

## Pointer Events

Now you probably wish there was a single set of events to handle both the iOS touch event model and the standard mouse events. Well, it turns out there really *is* a such thing.

<img src="/assets/images/articles/2013/04/pointer.png" alt="pointer" width="264" height="272" align="right" />


Microsoft has been working on something called MSPointers to support multi user-inputs, and they <a href="http://www.w3.org/TR/pointerevents" target="_blank">submitted</a> it to the W3C for standardization last year. Now it has reached the Last Call. This new and alternative standard event model is called Pointer Events, and it is designed to handle hardware-agnostic pointer input from devices like a mouse, pen, or touchscreen.

Besides Microsoft, Nokia, Google and Mozilla, are among the industry members working to solve this problem in the W3C Pointer Events Working Group.

This feature has been implemented already in Internet Explorer 10, and has been prototyped in the experimental version of Chromium.

The simple example below gets the x and y pointer coordinates using the pointer events. You will probably notice that the code looks similar to mouse events, which you may find less cumbersome compared with the touch events v1.  
<br style="clear:both" />

```javascript
canvas.addEventListener('pointerdown', function(e) {
var x = e.offsetX || e.layerX - canvas.offsetLeft;
var y = e.offsetY || e.layerY - canvas.offsetTop;
}, false);
```

&nbsp;

To support Internet Explorer 10 you need to use the prefixed version, so `pointerdown`, `pointermove` and `pointerup` event handler event types should be written as `MSPointerDown`, `MSPointerMove` and `MSPointerUP` respectively.

So <a href="https://dl.dropbox.com/u/1330446/tests/pointer-events.html" target="_blank">try this demo</a> on IE10 on desktop and/or Windows Phone 8.

## I <3 You All

As I mentioned earlier, at this moment the only available browsers that support the Pointer Events are IE10 and a prototype build of <a href="http://appendto.com/blog/2013/02/prototype-chromium-build-with-support-for-ms-pointer-events/" target="_blank">Chromium</a>, so it&#8217;s a good idea to include iOS touch events and mouse events until other browsers catch up.

```javascript
var downEvent = isTouchSupported ? 'touchstart' : (isPointerSupported ? 'MSPointerDown' : 'mousedown');

canvas.addEventListener(downEvent, function(e) {
var x = isTouchSupported ? (e.targetTouches[0].pageX - canvas.offsetLeft) : (e.offsetX || e.layerX - canvas.offsetLeft);
var y = isTouchSupported ? (e.targetTouches[0].pageY - canvas.offsetTop) : (e.offsetY || e.layerY - canvas.offsetTop);

}, false);
```


I have a <a href="https://dl.dropbox.com/u/1330446/demo/all-events.html" target="_blank">demo that supports all the methods</a> I&#8217;ve mentioned in the article.

Try this on any modern browser, and it should work! The entire code is <a href="https://gist.github.com/girliemac/5279460" target="_blank">in this gist</a> for you to take a look at.

<img alt="Screnshot" src="/assets/images/articles/2013/04/wp_ss_20130330_0001.png" width="320" style="float:left" />

<img src="/assets/images/articles/2013/04/qr-pointer-demo.png" alt="QR code" width="129" height="127" />

<br style="clear:both" />
---

## Learn More

*   W3C: <a href="http://www.w3.org/TR/touch-events/" target="_blank">Touch Events version 1</a>
*   MDN: <a href="https://developer.mozilla.org/en-US/docs/DOM/Touch_events" target="_blank">Touch events</a>
*   W3C: <a href="http://www.w3.org/TR/DOM-Level-3-Events/#events-mouseevents" target="_blank">Document Object Model (DOM) Level 3 Events Specification &#8211; Mouse Event Types</a>
*   W3C: <a href="http://www.w3.org/TR/pointerevents/" target="_blank">Pointer Events</a>
*   MSDN: <a href="http://http://msdn.microsoft.com/en-us/library/ie/hh673557(v=vs.85).aspx" target="_blank">Pointer and gesture events</a>