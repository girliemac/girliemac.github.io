---
title: 'CSS3 Aqua Button &#8211; Revisited for Firefox 3.6'
author: Tomomi Imura
layout: post
permalink: /blog/2010/01/28/css3-aqua-button-revisited-for-firefox-3-6/
categories:
  - CSS
  - Dev
  - Firefox
  - Sandbox
---
This is an update for the [Aqua button tutorial][1]. This update will add a support for Firefox 3.6. If you haven&#8217;t seen the article, please go read it before proceeding here.

  


[<img alt="Screenshot ot CSS Aqua buttons" src="/assets/images/wp-content/misc/screenshot_css3button_new.png" title="Screenshot" width="224" height="135" align="right" />][2]

On the end of November last year, <a href="http://hacks.mozilla.org/2009/11/css-gradients-firefox-36/" target="_blank">Mozilla Hacks announced</a> the support for CSS gradient in a background on upcoming Firefox 3.6 (which final version has just released recently). 

As already been supported on WebKit, FF does support both linear and radial gradient, however, Mozilla has implemented differently &#8211;  
Most noticeably, Mozilla separate linear and radial gradient as `-moz-linear-gradient` and `-moz-radial-gradient`, while on WebKit, the syntax goes `-webkit-gradient` and you specify linear or radial.

Also the specification of each value is different too.  
If you want a linear gradient starting from red on top to ending at bottom in white, you need to define &#8211; 

WebKit:  
```
background: -webkit-gradient(linear, left top, right bottom, from(red), to(white)))
```

Firefox:  
```
background: -moz-linear-gradient(top, red, white);<br />
```

### The Aqua Button Redefined

Let&#8217;s re-create the aqua button, by adding `-moz` prefixed gradient definitions:

The button:

```css
.aqua{
  background-color: rgba(60, 132, 198, 0.8);
  border-top-color: #8ba2c1;
  border-right-color: #5890bf;
  border-bottom-color: #4f93ca;
  border-left-color: #768fa5;	
  -webkit-box-shadow: rgba(66, 140, 240, 0.5) 0px 10px 16px;
  -moz-box-shadow: rgba(66, 140, 240, 0.5) 0px 10px 16px; 
  background-image: -webkit-gradient(linear, 0% 0%, 0% 90%, from(rgba(28, 91, 155, 0.8)), to(rgba(108, 191, 255, .9)));
/* for FF 3.6 */
  background-image: -moz-linear-gradient(rgba(28, 91, 155, 0.8) 0%, rgba(108, 191, 255, .9) 90%);
}
```

and the glare:

```css
.button .glare {
  position: absolute;
  top: 0;
  left: 5px;
  -webkit-border-radius: 8px;
  -moz-border-radius: 8px;
  height: 1px;
  width: 142px;
  padding: 8px 0;
  background-color: rgba(255, 255, 255, 0.25);
  background-image: -webkit-gradient(linear, 0% 0%, 0% 95%, from(rgba(255, 255, 255, 0.7)), to(rgba(255, 255, 255, 0)));
  /* for FF 3.6 */
  background-image: -moz-linear-gradient(rgba(255, 255, 255, 0.7) 0%, rgba(255, 255, 255, 0) 95%);
}
```

This is <a href="http://girliemac.com/sandbox/button.html" target="_blank">the actual html page</a>. Open it on Firefox 3.6 and see!

## More Info on Mozilla CSS Gradients

* <a href="http://hacks.mozilla.org/2009/11/css-gradients-firefox-36/" target="_blank">CSS gradients in Firefox 3.6</a> by HACKS.MOZILLA.ORG
* <a href="https://developer.mozilla.org/index.php?title=en/CSS/-moz-linear-gradient" target="_blank">-moz-linear-gradient</a> by Mozilla Developer Center
* <a href="https://developer.mozilla.org/index.php?title=en/CSS/-moz-radial-gradient" target="_blank">-moz-radial-gradient</a> by Mozilla Developer Center


 [1]: http://girliemac.com/blog/2009/04/30/css3-gradients-no-image-aqua-button/
 [2]: http://girliemac.com/sandbox/button.html