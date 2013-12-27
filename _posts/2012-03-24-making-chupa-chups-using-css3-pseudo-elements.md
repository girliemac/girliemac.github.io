---
title: Making Chupa-Chups using CSS3 Pseudo-elements
author: Tomomi Imura
layout: post
permalink: /blog/2012/03/24/making-chupa-chups-using-css3-pseudo-elements/
topsy_short_url:
  - http://is.gd/W2eAuB
  - http://is.gd/W2eAuB
categories:
  - CSS
---
One of the biggest reasons why I don&#8217;t blog often is probably because I tweet a lot. Just write a few words and throw some jsfiddle or Dabblet URLs in 140 chars, and boom, I can reach sizable numbers of people. It was quick and easy for me when I had busy days&#8230;

Well, now, I have lost my job at Hewlett-Packard (as they ditched Palm hardware then dumped the webOS software as open-source, they no longer need me and my hard-working teammates), so I should no longer excuse for not writing. So here I am, I decide to write up about CSS3 shapes from the fiddles I have written recently:

## Shapes with CSS3 Part.1 &#8211; Heart

<img src="/assets/images/wp-content/uploads/2012/03/css3-valentine.png" alt="CSS3 Valentine's heart-shaped chocolate" title="css3-valentine" width="200" height="200" align="left" /> 

Heart-shaped chocolate live demo: <a href="http://codepen.io/girliemac/pen/xkiDz" target="_blank">http://codepen.io/girliemac/pen/xkiDz</a>

This Valentine's Day demo (I really did make this on Feb.14!) shows how to create a heart shape.  
Basic idea behind is that creating two rectangles with round-corners on top-left and top-right, and rotate each object in either positive or negative 45 degrees. The trick of making two objects in one HTML element is using pseudo-elements, `::before` and `::after`.  
This code snipet shows how to create a simple heart-shape:<br clear="both" />

```css
.heart {
	position: relative;
}
.heart::before,
.heart::after {
	content: "";
	position: absolute;
	top: 0;
	background-color: red;
	width: 150px;
	height: 240px;
	border-radius: 75px 75px 0 0;
}
.heart::before {
	left: 0px;
	transform: rotate(-45deg);
	background-color: red;
}
.heart::after {
	left: 64px;
	transform: rotate(45deg);
}
```

In this example, I omit the vender prefix, but you do need to include them, for example, `-webkit-transform` to be able to make this code work on the current browsers.

## Shapes with CSS3 Part.2 &#8211; Flower

<img src="/assets/images/wp-content/uploads/2012/03/css3-chupachups.png" alt="css3 Chupa Chups" title="css3-chupachups" width="200" height="200" align="left" /> 

Chupa-Chupsy live demo: <a href="http://codepen.io/girliemac/pen/gnfwd" target="_blank">http://codepen.io/girliemac/pen/gnfwd</a>

This Chupa-Chups, or I&#8217;d call it Chupa-Chupsy candy, since I cannot replicate the actual design of the candy wrapper accurately. (Oh, by the way, did you know the logo was created by the surreal artist, Salvador Dalí? <a href="http://www.fastcodesign.com/1669224/salvador-dal-s-real-masterpiece-the-logo-for-chupa-chups-lollipops" target="_blank">Seriously</a>.)

So I tried to mimic the signature yellow flower-shape, with one HTML element using the pseudo-element. This shape is made with a combination of two rounded-corner squares. One of the square is rotated to 45 degrees.  
This is how to create the basic flower-shape:

```css
.flower-shape {
    position: relative;
}
.flower-shape,  
.flower-shape::before {
    width: 200px;       
    height: 200px;
    border-radius: 25%;
    background: yellow;
}
.flower-shape::before {
    content: "";
    position: absolute;
    transform: rotate(45deg);
}
```

In this example, I used only `::before` pseudo-element, instead of both *before* and *after*. Although I used both for the heart-shape example (which is made with two rectangles), technically, you can include three objects into one HTML element by inserting each object before and after the object on the element. 

So if you&#8217;d like to have a flower with 12 petals, you can define `.flower-shape::after`, which is rotated in 30deg. Make sure to make the `.flower-shape::before` in -30deg.

To mimic the candy logo, I used the most similar web-font I found on <a href="http://www.google.com/webfonts" target="_blank">Google Web Font</a>. Once you see the real Chupa-Chups logo, you&#8217;ll see this web-font is actually nothing resembling it. But, hey.

## Shapes with CSS3 Part.3 &#8211; Speech Bubble

<img src="/assets/images/wp-content/uploads/2012/03/css3-klout.png" alt="Klout flag" title="css3-klout" width="200" height="180" align="left" />

Klout Score Flag demo: <a href="http://jsfiddle.net/girlie_mac/2uk6U/" target="_blank">http://jsfiddle.net/girlie_mac/2uk6U/</a>

This is a no-image replica of the <a href="http://klout.com/girlie_mac" target="_blank">Klout</a> score flag! Creating this speech-bubble style shape used the same technique using `::after` pseudo-element.  
The method of making the triangle shape is the good&#8217;ol CSS2 border shading trick using border-width and border-color. Giving think borders around a box with zero width and height. The triangle size is determined by the border-width, with the given color on the one side and transparent on the rest of the sides. You can read more about how to create a triangle on <a href="http://css-tricks.com/snippets/css/css-triangle/" target="_blank">CSS-Tricks.</a>

The basic shape can be coded like this:

```css
.speech {
    background-color: orange;
    width: 200px;
    height: 160px;
    border-radius: 10px;
    position: relative;
}
.speech:after {
    content: "";
    display: block;
    width: 0;
    height: 0;
    border-bottom: 28px solid transparent;
    border-right: 58px solid orange;
    position: absolute;
    right: 0;
}
```