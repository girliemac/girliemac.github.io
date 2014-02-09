---
title: Webkit CSS 3D + Local DB Demo
author: Tomomi Imura
layout: post
permalink: /blog/2009/09/03/webkit-css-3d-local-db-demo/
dsq_thread_id:
  - 2067976836
categories:
  - CSS
  - Dev
  - iPhone
  - Sandbox
  - WebKit
---
![css 3D screenshot][1]

Ever since I heard of Snow Loepard's hardware-accelerated CSS, I wanted try some cool CSS animation for Safari 4.

So after installing Snow Leopard, I spent about a day and half to try creating my first 3D animation with Flickr API.  
Honestly, I wasn't sure where to get started to make some cool 3D effect, so what I did was I tried to reproduce the one on webkit.org example and modify a lot by trial and error approach.  
Also, I have been freqently asked about how I did with &#8220;My Favorites&#8221; feature on [my Palm Pre app][2] (which is also a WebKit-based), so I throw the HTML5&#8242;s local storage demo with this 3D demo. 

So here, you can try my <a href="http://girliemac.github.io/flickr-css3-3d-demo/" target="_blank">CSS 3D and Local DB Demo</a>!!!  
Be sure to view this demo on Safari 4, iPhone Safari, or WebKit Nightly! This doesn;t seem to work on other Webkit-based browsers such as Chrome and Palm. 

I am not going to write a whole tutorial how to replicate this animation but I try to explain some examples.

## Spin a Wheel!

Look at one of the flicke photo wheel on my demo. This is a combination of a few different animation.  
Let&#8217;s focus on the small wheel inside. This is the snippet of HTML of the wheel:

```html
<div id="gallery">
  <div id="pic01"><img src="..."/></div>
  <div id="pic02"><img src="..."/></div>
  ... (10 more imgs)
</div>	
	
```

<img src="/assets/images/wp-content/misc/coordinate.png" alt="3D Cood" align="left" />  
OK, for now, let&#8217;s ignore how each photo is rendered to form a loop, and just focus on the animation of one div, #gallery (= a wheel). A band of photos is ratating clockwise around Y-axis.  
This means the animation starts as `-webkit-transform: rotateY(0);` and goes around an circle for a whole 360 degree. ` -webkit-transform: rotateY(-360deg);`.  
Use positive if you want to rotate in opposite direction.  
I set the whole circle completion span as 60 seconds in linier motion and the animation goes infinite. 

This diagram from <a href="http://developer.apple.com/safari/library/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Transforms/Transforms.html" target="_blank">Apple&#8217;s Safari Reference Library</a> explains coordinates.

So the css for this movement is defined as:

```css
#gallery {
  -webkit-transform-style: preserve-3d;
  -webkit-animation: spinY 60s linear infinite; 
}
```

```css
@-webkit-keyframes spinY {
  from { -webkit-transform: rotateY(0);}
  to   { -webkit-transform: rotateY(-360deg);}
}
```

Use 3D style, `-webkit-transform-style: preserve-3d;`to give 3D illusion. I set the initial perspective in its parent div as `-webkit-perspective: 380;`.  
It gives you an illusion of the depth. You can make the value lower to make it look more up-close to you.  
The unit of perspective should be &#8220;px&#8221;, but it looks like you&#8217;d better remove it for iPhone.

![perspective 200][3] ![perspective 400][4]  
![perspective 500][5] ![perspective 0][6]

To figure out how to render each photo in loop, also other animations, please look at the source code of my demo.

Also, I will write about how to use HTML 5&#8242;s local storage sometimes later!

## References

*   <a href="http://webkit.org/blog/386/3d-transforms/" target="_blank">3D Transforms</a> by Webkit.org
*   <a href="http://webkit.org/blog/130/css-transforms/" target="_blank">CSS Transforms (2D)</a> by Webkit.org
*   <a href="http://webkit.org/blog/138/css-animation/" target="_blank">CSS Animation</a> by Webkit.org
*   <a href="http://www.w3.org/TR/css3-3d-transforms/" target="_blank">CSS 3D Transforms Module Level 3</a> W3C Working Draft
*   <a href="http://developer.apple.com/safari/library/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Transforms/Transforms.html" target="_blank">Safari Reference Library -Transforms</a> by Apple

 [1]: /assets/images/wp-content/misc/css3d.jpg
 [2]: http://girliemac.com/blog/2009/08/29/pretty-cute-suite-another-cute-app-for-pre-from-me/
 [3]: /assets/images/wp-content/misc/css3d_pers200.png
 [4]: /assets/images/wp-content/misc/css3d_pers400.png
 [5]: /assets/images/wp-content/misc/css3d_pers500.png
 [6]: /assets/images/wp-content/misc/css3d_pers0.png