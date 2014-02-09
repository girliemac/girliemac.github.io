---
title: 'CSS3 Box-Shadow with Inset Values &#8211; The Aqua Button ReReVisited!'
author: Tomomi Imura
layout: post
permalink: /blog/2010/02/04/css3-box-shadow-with-inset-values-the-aqua-button-rerevisited/
categories:
  - CSS
  - Dev
  - Firefox
  - Opera
  - Sandbox
  - WebKit
---
[<img alt="Screenshot ot CSS Aqua buttons" src="/assets/images/wp-content/misc/screenshot_css3button_2.png" title="Screenshot" width="224" height="135" align="right" />][1]

This is my third article on CSS3 No Image Aqua Buttons. The previous articles include:

1.  <a href="http://girliemac.com/blog/2009/04/30/css3-gradients-no-image-aqua-button/" target="_blank">CSS3 Gradients: No Image Aqua Button</a>
2.  <a href="http://girliemac.com/blog/2010/01/28/css3-aqua-button-revisited-for-firefox-3-6/" target="_blank">CSS3 Aqua Button – Revisited for Firefox 3.6</a>
3.  And this one &#8211; Read on!

Since Smashing Magazine has selected the original Aqua button demo for their article, <a href="http://www.smashingmagazine.com/2010/02/01/50-brilliant-css3-javascript-coding-techniques/" target="_blank">&#8220;50 Brilliant CSS3/JavaScript Coding Techniques&#8221;</a>, I have had so much more visitors to my blog. 

This resulted quality developers leave useful comments and tips for me &#8211; thank you, <a href="http://girliemac.com/blog/2010/01/28/css3-aqua-button-revisited-for-firefox-3-6/#comment-1411" target="_blank">Zoley</a> for suggesting using `box-shadow` with the *inset* value, and a big thank you to <a href="http://girliemac.com/blog/2010/01/28/css3-aqua-button-revisited-for-firefox-3-6/#comment-1428" target="_blank">Jim</a> for actually re-writing the Aqua button with the technique!!!

So, now the CSS3 Aqua button is revised with semantic markup (no more &#8220;glare&#8221; div! Yes, I complained it by myself before!) and shorter CSS.  
And this time, no CSS gradients! &#8211; use CSS `box-shadow` property with multiple *inset* values to draw layers of inner-shadows to create the visual effect.

### Syntax

```
box-shadow: none | [inset? && [ <offset-x> <offset-y> <blur-radius>? <spread-radius>? <color>? ] ]#
```

### Values

from <a href="https://developer.mozilla.org/en/CSS/-moz-box-shadow" target="_blank">Mozilla Developer Center</a>:

**inset (optional)**  
If not specified (default), the shadow is assumed to be a drop shadow (as if the box were raised above the content).  
The presence of the `inset` keyword changes the shadow to one inside the frame (as if the content was depressed inside the box). Inset shadows are drawn above background, but below border and content.  
  
**<color> (optional)**  
If not specified, the color depends on the browser. In Gecko (Firefox), the value of the `color` property is used. Safari&#8217;s shadow is transparent and therefore useless if <color> is omitted.  
  
**<offset-x> <offset-y> (required)**  
This are two <length> values to set the shadow offset. <offset-x> specifies the horizontal distance. Negative values place the shadow to the left of the element. <offset-y> specifies the vertical distance. Negative values place the shadow above the element.  
If both values are 0, the shadow is placed behind the element (and may generate a blur effect if <blur-radius> and/or <spread-radius> is set).  
   
**<blur-radius> (optional)**  
This is a third <length> value. The higher this value, the bigger the blur, so the shadow becomes bigger and lighter. If not specified, it will be 0.  
  
**<spread-radius> (optional)**  
This is a fourth <length> value. Positive values will cause the shadow to expand and grow bigger, negative values will cause the shadow to shrink. If not specified, it will be 0 (the shadow will be the same size as the element).  


Note &#8211; The `box-shadow` property has been removed from <a href="http://www.w3.org/TR/css3-background/#the-box-shadow" target="_blank">W3C CSS3 Background</a> Candidate recommendation document.

### The Entire Code!

Use `-moz` and `-webkit` prefix for `box-shodow` to support these browsers. For Opera, there&#8217;s no need to add `-o`.

Also, notice there are three `inset` values are defined for detailed visual effects!

```html
<input type="button" class="new-aqua" value="Login">
```

```css
input[type=button].new-aqua {
  width: 155px;
  height: 35px;		
  background: #cde; 
  border: 2px solid #ccc; 
  border-color: #8ba2c1 #5890bf #4f93ca #768fa5; 
  font: 600 16px/1 Lucida Sans, Verdana, sans-serif; 
  color: #fff; 
  text-shadow: rgba(10, 10, 10, 0.5) 1px 2px 2px;
  text-align: center; 
  vertical-align: middle; 
  white-space: nowrap; 
  text-overflow: ellipsis; 
  overflow: hidden;
  border-radius: 16px; -moz-border-radius: 16px; -webkit-border-radius: 16px;
  box-shadow: 0 10px 16px rgba(66, 140, 240, 0.5), inset 0 -8px 12px 0 #6bf, inset 0 -8px 0 8px #48c, inset 0 -35px 15px -10px #7ad;
  -moz-box-shadow: 0 10px 16px rgba(66, 140, 240, 0.5), inset 0 -8px 12px 0 #6bf, inset 0 -8px 0 8px #48c, inset 0 -35px 15px -10px #7ad;
  -webkit-box-shadow: 0 10px 16px rgba(66, 140, 240, 0.5), inset 0 -8px 12px 0 #6bf, inset 0 -8px 0 8px #48c, inset 0 -35px 15px -10px #7ad;
}
.new-aqua:hover {
  text-shadow: rgb(255, 255, 255) 0px 0px 5px;
}
```

  


View the <a href="https://dl.dropboxusercontent.com/u/1330446/demo/button.html" target="_blank">live demo page</a>! This new aqua button works on FF 3.6, Webkit 4 (the current Safari 4 doesn&#8217;t support inset box-shadow yet), Chrome 4 and Opera 10. (But fails on 10.1 on Mac).

<p style="color:#777">
  <em>* Edited on Feb.5 &#8211; Opera 10.1 fail and Safari4 (I noticed this works only on Webkit Nightly after published this!)</em>
</p>

And again, a huge thanks to <a href="www.coroflot.com/trickitty" target="_blank">Jim Green</a> for the revised CSS!

## References

* <a href="http://developer.apple.com/safari/library/documentation/AppleApplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html" target="_blank">Safari CSS Reference</a> by Apple Safari Dev Center
* <a href="https://developer.mozilla.org/en/CSS/-moz-box-shadow" target="_blank">-moz-box-shadow</a> by Mozilla Developer Center
* <a href="http://dev.opera.com/articles/view/css3-border-background-boxshadow/" target="_blank">CSS3 borders, backgrounds and box-shadows</a> by Dev.Opera


 [1]: http://girliemac.com/sandbox/button.html