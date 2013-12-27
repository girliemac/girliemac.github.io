---
title: 'CSS3 Gradients: No Image Aqua Button'
author: Tomomi Imura
layout: post
permalink: /blog/2009/04/30/css3-gradients-no-image-aqua-button/
dsq_thread_id:
  - 2067751853
  - 2067751853
categories:
  - CSS
  - Firefox
  - Sandbox
  - WebKit
  - Yahoo!
---
<p style="color:red">
  <em>Note (Jan 28, 2010): I added a Firefox support to this tutorial. Please visit the <a href="http://girliemac.com/blog/2010/01/28/css3-aqua-button-revisited-for-firefox-3-6/">&#8220;revisited&#8221;</a> article too!</em>
</p>

Boooo, Yahoo! just had the 3rd round of layoff within a little over a year period, and this time I was axed with several more fellow excellent engineers of Mobile team. So now I have free time to spend on more coding!  
My job function needed full focus on products and it prevented me to have experiments and testing as I wanted to, so I always spent my own time to do. Now I can do whatever I want to while I am still on payroll. Yes! I am still paid my regular salary for a while, thanks for the new regulation <img src='http://girliemac.com/blog/wp-includes/images/smilies/icon_smile.gif' alt=':-)' class='wp-smiley' /> 

<img src="/assets/images/wp-content/misc/screenshot_css3button.png" alt="css3 button screenshot" align="right" />  
OK, enough blah about the stupid corporate stuff.  
Anyway, I played around with WebKit CSS3 gradient and created a useless but fun stuff &#8211; an Aqua button with no images!  
Back in the time when Mac OS X was first announced, there&#8217;re a plenty of web tutorials that describe how to create the sexy aqua button with Photoshop, and now I can show how to create one with CSS! 

Here&#8217;s a screen capture of the rendered button. You can see <a href="http://girliemac.com/sandbox/button.html" target="_blank">the actual HTML page</a> too. 

OK, let&#8217;s take a look at the code:

```html
<div class="button aqua">	
  <div class="glare"></div>
  Button Label
</div>
```

## Create a Button Base and Styling Label

```css
.button{
  width: 120px;
  height: 24px;
  padding: 5px 16px 3px;
  -webkit-border-radius: 16px;
  -moz-border-radius: 16px;
  border: 2px solid #ccc;
  position: relative;
	
  /* Label */
  font-family: Lucida Sans, Helvetica, sans-serif;
  font-weight: 800;
  color: #fff;
  text-shadow: rgba(10, 10, 10, 0.5) 1px 2px 2px;
  text-align: center;
  vertical-align: middle;
  white-space: nowrap;
  text-overflow: ellipsis; 
  overflow: hidden;
}
```

The first part to render a rounded-corner rectangle. Set the position as relative to place &#8220;glare&#8221; inside of the button later.  
The second part is for styling the label.  
Give text-shodow with alpha-transparency. (Believe or not, Chrome and Android do not support text-shadow!) 

## Button Color and Shadow

```css
.aqua{
  background-color: rgba(60, 132, 198, 0.8);
  background-image: -webkit-gradient(linear, 0% 0%, 0% 90%, from(rgba(28, 91, 155, 0.8)), to(rgba(108, 191, 255, .9)));
  border-top-color: #8ba2c1;
  border-right-color: #5890bf;
  border-bottom-color: #4f93ca;
  border-left-color: #768fa5;	
  -webkit-box-shadow: rgba(66, 140, 240, 0.5) 0px 10px 16px;
  -moz-box-shadow: rgba(66, 140, 240, 0.5) 0px 10px 16px; /* FF 3.5+ */
}
```

Now, specify the appearance of the button and shadow at bottom.  
Here. I use the `-webkit-gradient` to create a nice-looking aqua gradient.

Notice that I use `-webkit-gradient` as a `background-image`, although there&#8217;s no physical graphics are added there.  
You can use gradients in `background-image`, `border-image`, `list-style-image` and content property.  
On Firefox, this is ignored and you see only Background-color. 

The syntax for linear gradient is as follows:  
  
```css
-webkit-gradient(lenear, left top, right bottom, from(start color/alpha), to(end color/alpha))
``` 

In this example, starts with dark blue from straight top to bottom (no angle) at 95%, not all way down, to blended into lighter blue. 

Then, I specified color on each border (so the css looks pretty messy).

Finally, give a nice shadow at bottom, with `-webkit-box-shadow`.  
Firefox 3.5+ supports it too, so duplicate it with `-moz-box-shadow`.

Syntax is as:  
  
```css
[color/alpha] [horizontal offset] [vertical offset] [blur radius] 
``` 

## Give it shine

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
}
```

The class *glare* renders the glossy look on the button.  
First, give absolute position to the parent container, `button` to give shine in the right position. 

 
Again, use `-webkit-gradient` to create the glossy look, by playing with alpha-transparency.  
Start with the white (alpha 0.7) and end with complete transparent (alpha 0). 

Honestly, I do not like to have this non-semantic empty div block to only get this visual effect.  
I need to figure a better way to do.

## References:

*   <a href="http://devworld.apple.com/safari/library/documentation/AppleApplications/Reference/SafariCSSRef/Articles/Functions.html#//apple_ref/doc/uid/TP40007955-SW25" target="_blank">Safari Reference Library &#8211; CSS Property Functions</a> by Apple
*   <a href="http://webkit.org/blog/175/introducing-css-gradients/" target="_blank">Surfin&#8217; Safari &#8211; Introducing CSS Gradients</a>
*   <a href="https://developer.mozilla.org/en/CSS_Reference/Mozilla_Extensions" target="_blank">Mozilla Extensions</li> </ul>