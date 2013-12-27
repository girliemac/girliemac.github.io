---
title: Five CSS tricks used in Enyo JS Framework, and you can try them too!
author: Tomomi Imura
layout: post
permalink: /blog/2011/07/29/five-css-tricks-used-in-enyo/
topsy_short_url:
  - http://is.gd/0BiS8L
  - http://is.gd/0BiS8L
categories:
  - CSS
  - Dev
  - Palm
  - WebKit
---
Since I have joined Palm (now HP), I don&#8217;t blog frequently because working for the webOS have kept me super busy. Especially when working on the webOS 3.0 for the Touchpad tablet, I have been in multiple teams until I switched my position to commit for the Developer Relations team. 

Anyway, in case you are not familiar with webOS and Enyo &#8211; webOS is a mobile platform running on Linux kernel/ webkit UI with V8 engine, so most of core apps are either written in JS and CSS, or native C/C++. And the JS framework for 3.0 is called ***Enyo***. Basically working on the webOS framework and apps is just like developing web (in fact, I use Chrome for development). So here, I want to share some cool CSS tracks used in the framework! 

## 1. Flexible Box Model

Enyo's basic UI is created with using the <a href="http://www.w3.org/TR/css3-flexbox/" target="_blank">CSS3 flexible box model</a>.  
You no longer have to worry about all the `float` craziness. I actually have written an article, **<a href="http://developer.palm.com/blog/2011/07/css-3-flexible-box-model-and-enyo-flex-layout/" target="_blank">CSS 3 Flexible Box Model and Enyo Flex Layout</a>** for webOS Developer Blog too, so please read it too! 

#### Example:

When you want to achieve a layout that has an avatar at the left, and two lines of a person&#8217;s info at the right side like this,  


<img src="/assets/images/wp-content/uploads/2011/07/flexbox-tweets.png" alt="flex box demo" title="flexbox-tweets" style="border: 1px dotted #ccc; border-radius: 10px; padding:.5em" />  


You can create this UI without float if the browser support flex-box:

```html
<div class="tweet">
  <div class="tweet-avatar"><img src="avatar.png"></div>
  <div class="tweet-contents">
    <div class="tweet-username">@n00b_css3_user</div>
    <div class="tweet-text">Hello, world. CSS3 Flexbox is cool.</div>
  </div>
</div>
```


```css
.tweet {
  display: -webkit-box;
  -webkit-box-orient: horizontal;	
}

.tweet-contents {
  margin-left: .5em;
  display: -webkit-box;
  -webkit-box-flex: 1;
  -webkit-box-orient: vertical;
  -webkit-box-pack: center;
}
```

Note: this is an original spec from 2009 and this is what browsers currently support (if they do), and likely to keep supporting. I have no idea why the spec has been completely re-written recently, but so far no browsers support the new specs.

## 2. Root Em 

There is a new unit in CSS, **`rem`** unit, which stands for &#8220;root em&#8221;. The sizing only with `em` could be troublesome because how it relates to the parent&#8217;s font-size. However, the `rem` is relative to the root, which is html.  
In Enyo framework, the root font size is set to 20px. So by using `rem`, you can set its children font-size easily without being affected by their parents. 

Here&#8217;s a comparison of em and rem: 

```html
<div class="container">
  <p class="subdue">48 minutes ago</p>
</div>
```

With `em`

```css
html {font-size: 20px;}
.container {font-size: .8em}
.subdue {font-size: .75em} /* the font size = 12px (20 x .8 x .75) */
```

With `rem`

```css
html {font-size: 20px;}
.container {font-size: .8em}
.subdue {font-size: .75rem} /* the font size = 15px (20 x .75) */
```

## 3. Pointer-events

This is a little obscure and simple trick not everybody has known, and a secret(?) trick I have been using since the earlier webOS framework called Mojo.  
The `pointer-events` property was originally defined for SVG content, and later adopted as a CSS property.  
For CSS, there are only two values: `auto` or `none`.  
You can control the target of the mouth event, and by setting this value none, the element is no longer a target of mouse events, so when a user click the element, it pass through to its descendant during the event bubbling. 

```html
<div style="position:relative">
  <div class="overlay"></div>
  <ul>
    <li><a href="">link 1 on fading list</a></li>
    <li><a href="">link 2 on fading list</a></li>
    <li><a href="">link 3 on fading list</a></li>
  </ul>
<div>
```

```css
.overlay {
  pointer-events: none;
}
```

The screenshots at left indicates that when the `pointer-events` property value is not set (default), the first link underneath of the visual overlay is not clickable, and when it is set none, the element becomes clickable (right). 

![pointer-events demo][1]

The demo: <a href="http://jsfiddle.net/girlie_mac/7TvVY/" target="_blank">http://jsfiddle.net/girlie_mac/7TvVY/</a> 

## 4. border-image with sprites

You have seen some demos how to use the CSS3 `border-image`.  
But making multiple assets used for `border-image` is trivial because how an image needs to be &#8220;sliced&#8221; into 9 tiles with css.  
However, if an each asset in the sprites only requires into 3 tiles. (For example, \[static-left\] \[stretchable center\] [static-right], and top and bottom borders are zero, you can create a single sprite image of multiple states of a button, and still be able to achieve the `border-image`. 

```css
.alert-button {
  /* notice the fat border-bottom */
  -webkit-border-image: url(images/alert-button.png) 0 14 111 14 repeat repeat;
  
  /* notice that border-top and bottom are set zero */
  border-width: 0 14px;

  /* some visual styling here */
  -webkit-box-sizing: border-box;
  height: 37px;
  line-height: 37px;
}

.alert-button:active {
  /* the fat border-top and bottom adjusted */
  -webkit-border-image: url(images/alert-button.png) 37 14 74 14 repeat repeat;
}
```

<img src="/assets/images/wp-content/uploads/2011/07/border-img-button1.png" alt="border-image demo" title="border-img-button" width="588" height="574" align="left" size-full style="margin-right:1em" wp-image-313" /> 

The demo: <a href="http://jsfiddle.net/girlie_mac/89C2T/" target="_blank">http://jsfiddle.net/girlie_mac/89C2T/</a> 

## 5. Hardware acceleration

WebKit enables hardware-acceleration to render CSS 3D transforms. Although some WebKit (like webOS) may not render 3D visuals correctly, it still uses the GPU to speed up. So all you need to take advantage of this is to use the `-webkit-transform` <a href="http://www.w3.org/TR/css3-3d-transforms/" target="_blank">CSS property</a>!  
The easiest possible way to achieve it is using `translate3d` instead of `translate` (also `scale3d` instead of `scale`), although you are not intend to make your web in 3D visual effect. 

```css
.toaster {
  -webkit-transform: translate3d(0,0,0);
}
```

or just set only the z-axis:

```css
.toaster {
  -webkit-transform: translateZ(0);
}
```

  


I hope some of the stuff I just wrote are new to you!  
There are more fun stuff I can write about Enyo JS framework, but I keep them for the official <a href="http://developer.palm.com/blog" target="_blank">HP webOS Dev Blog</a>!

Bye now!

 [1]: /assets/images/wp-content/uploads/2011/07/pointer-events.png "pointer-events"