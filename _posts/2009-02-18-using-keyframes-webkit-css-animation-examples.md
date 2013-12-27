---
title: 'Using Keyframes &#8211; WebKit CSS Animation Examples'
author: Tomomi Imura
layout: post
permalink: /blog/2009/02/18/using-keyframes-webkit-css-animation-examples/
dsq_thread_id:
  - 2067799945
categories:
  - CSS
  - Dev
  - iPhone
  - Sandbox
  - WebKit
---
Now WebKit supports explicit CSS animations! After seeing the new animation examples posted on <a href="http://webkit.org/blog/324/css-animation-2/" target="_blank">WebKit.org</a>, I needed to test `keyframes` by myself.  
So I have created a dumb-downed version of the fallen leaves seen on webkit.org <a href="http://webkit.org/blog-files/leaves/index.html" target="_blank">blog</a>, called &#8220;Let it Snow&#8221;.

Unlike the fallen leaves example, I stick strictly with CSS only (means zero JavaScript). Also I tested on Webkit nightly and an iPhone (OS 2.0) Safari. On my iPhone (<code class="small">Mozilla/5.0 (iPhone; U; CPU iPhone OS 2_2 like Mac OS X; en-us) AppleWebKit/525.18.1 (KHTML, like Gecko) Version/3.1.1 Mobile/5G77 Safari/525.20</code>), the animation is slow and some feature is ingored. 

Well, let&#8217;s see the &#8220;Let It Snow&#8221; animation <a href="http://girliemac.com/sandbox/snow.html" target="_blank">in action!</a>

## How to use Keyframes?

Keyframes are specified with the CSS &#8220;At-Rule&#8221; by using the keyword,**@-webkit-keyframes**, followed by an identifier (= *animation-name*)

```css
@-webkit-keyframes <em>animation-name {
 from {
   style definition ["Before"-state]
 }
 to {
   style definition ["After"-state]
 }
}
```

A keyframe defines the styles applied within the animation. To specify multiple frames, use &#8220;%&#8221; instead of &#8220;from&#8221; and &#8220;to&#8221; keywords.  
Here&#8217;s an actual example I used for &#8220;Let it Snow&#8221;.

```css
@-webkit-keyframes fade {
  0%   { opacity: 0; }
  10%  { opacity: 0.8; }
  100% { opacity: 0; }
}
```

This style is applie to create each snow flake appearance. A snowflake blurry appears (increase opacity) when 10% of the time elapsed (The total time is defined later. I&#8217;ll explain it next).  
And at the end, the snowflake disappears (opacity back to zero).

Once the animation timeframe is defined, apply it using -webkit-animation-name and related properties.  
I set total animation duration as 5 seconds, and the animatin goes forever (= *infinite* times. The default is 1).  
See the simplified example below.

```css
#snow div {
  -webkit-animation-name: fade;
  -webkit-animation-duration: 5s;
  -webkit-animation-iteration-count: infinite;
}
```

```html
<div id="snow" class="snow">	
  <div>&#10053;</div> /* an entity for &#10053; */
</div>
```

## Using Transform

Let&#8217;s rotate and move around snowflakes by using <code class="small">-webkit-transform</code>.  
<code class="small">rotate</code>, of course, rotate the element, and <code class="small">translate</code> specifies a 2D translation by the vector [tx, ty]. (For more explanations, please see <a href="http://webkit.org/specs/CSSVisualEffects/CSSTransforms.html" target="_blank">CSS transform spec</a> page).  
I used percent, 0 and 100% here, but of course you can use &#8220;from&#8221; and &#8220;to&#8221;.  
Also note that <code class="small">transform</code> doesn&#8217;t seem to work on current iPhone Safari yet.

```css
@-webkit-keyframes spin{
  0%   { -webkit-transform: rotate(-180deg) translate(0px, 0px);}
  100% { -webkit-transform: rotate(180deg) translate(10px, 75px);}
}			
```

You can just add the amination-name to the #snow div selector, separating with comma.

```css
#snow div {
  -webkit-animation-name: fade, spin;
  ...
}
```

## More

For the &#8220;Let it snow&#8221; example, I also include the cheesy &#8220;accumulate&#8221; keyframe to make snow accumulate on ground. Kinda ugly though.  
Moreover, I gave the <code class="small">-webkit-animation-duration</code> to individual snowflake so all flakes don&#8217;t fall all together! 

```css
.snowflake {
  color: #fff;
  font-size: 2em;
  position: absolute; (Note: The parent container is set relative positioned!)
}
.snowflake.f1 {
  left: 40px;
  -webkit-animation-duration: 5s;
}
.snowflake.f2 {
  font-size: 1.8em;
  left: 120px;
  -webkit-animation-duration: 7s;	
}
...
```

```html
<div id="snow" class="snow">	
  <div class="snowflake f1">&#10053;</div> /* an entity for &#10053; */
  <div class="snowflake f2">&#10052;</div> /* an entity for &#10052; */
  ... /* add two more snowflake-div in the actual sample) */
</div>
```

To view the entire markup and CSS, just view source of the <a href="http://girliemac.com/sandbox/snow.html" target="_blank">sample file</a>!



## Resources

*   <a href="http://webkit.org/blog/138/css-animation/" target="_blank">Surfin&#8217; Safari &#8211; CSS Animation</a>
*   <a href="http://webkit.org/blog/324/css-animation-2/" target="_blank">Surfin&#8217; Safari &#8211; CSS Animation 2</a>
*   <a href="http://webkit.org/specs/CSSVisualEffects/CSSAnimation.html" target="_blank">CSS Effects proposed specifications &#8211; Animation</a>
*   <a href="http://webkit.org/specs/CSSVisualEffects/CSSTransforms.html" target="_blank">CSS Effects proposed specifications &#8211; Transforms</a>
*   <a href="http://developer.apple.com/documentation/appleapplications/Reference/SafariCSSRef/Articles/StandardCSSProperties.html#//apple_ref/doc/uid/TP30001266-VisualEffects" target="_blank">Safari Supported CSS Properties &#8211; &#8220;Visual Effects&#8221;</a>
*   <a href="https://developer.apple.com/webapps/docs/samplecode/CardFlip/" target="_blank">Apple Web Apps Reference Library &#8220;CardFlip&#8221;</a> (Registration required)