---
title: Simulating MacOS Dock-like menu with CSS3
author: Tomomi Imura
layout: post
permalink: /blog/2010/06/02/simulating-macos-dock-like-menu-with-css3/
categories:
  - CSS
  - Dev
  - Firefox
  - iPhone
  - Sandbox
  - WebKit
---
![css3 Dock screenshot][1]

Since my original &#8220;CSS Aqua button&#8221; written last year, I have seen more and more fan CSS3 UI mimic of MacOS components around! I think I have seen some Mac docks too, but as I remember they all use jQuery.  
So I was thinking about making one only with CSS. 

Initially I thought it was easy &#8211; let&#8217;s make an hovered icon larger like 200%, and make siblings in 150% of the original size using CSS sibling selector, and done! A piece of cake, huh? &#8211; Then I realized I made a mistake. The adjacent-sibling selector apply to an element which is immediately *after* the element in markup, not both before and after.  
Oh well, so I needed to write a minimal JavaScript (so you don&#8217;t need to import a whole JS library) to add a class name to the element comes before the hovered object.

Anyway, here&#8217;s the <a href="https://dl.dropboxusercontent.com/u/1330446/demo/dock/dock.html" target="_blank">live-demo!</a> (Try it with the the latest Webkit Nightly or Safari 4) for the best experience!), and I&#8217;ll show you how I did- 

### Markup (Simplified)

Let&#8217;s create menu items as a list.

```html
<div id="dock-container">
  <div id="dock">
  <ul>
    <li><a href="http://android.com"><img src="images/dock-icons/android.png"/></a></li>
    <li><a href="http://palm.com"><img src="images/dock-icons/palm.png"/></a></li>
    <li>...
  </ul>
  <div class="base"></div>
  </div>
</div>
```

The list should be displayed horizontally by setting the style to `#dock li {display:inline-block}`. Please see the source code from the demo for the details. 

### Magnify the icon with CSS transform

<img style="border:1px solid #666;" src="/assets/images/wp-content/misc/dock-tutorial.png" align="right" />First, let&#8217;s define the dock icon animation with css transition.  
The origin of the transform has to set to bottom, so the icon doesn&#8217;t scale from the middle of the icon. (Diagram #1).

I used only a webkit extension for this example but you can use `-moz` and `-o` extensions, for Firefox and Opera respectively.

Then, set the hover state &#8211; use css transform to scale the icon image up to 200%. Also you need to add some margin otherwise the enlarged icon overlaps with neighboring icons! 

```css
#dock li img {
  width: 64px;
  height: 64px;
  -webkit-box-reflect: below 2px
		    -webkit-gradient(linear, left top, left bottom, from(transparent),
		    color-stop(0.7, transparent), to(rgba(255,255,255,.5))); /* reflection is supported by webkit only */
  -webkit-transition: all 0.3s;
  -webkit-transform-origin: 50% 100%;
}
#dock li:hover img { 
  -webkit-transform: scale(2);
  margin: 0 2em;
}
```

### Magnify adjacent icons

```css
#dock li:hover + li img,
#dock li.prev img {
  -webkit-transform: scale(1.5);
  margin: 0 1.5em;
}
```

To magnify the icon at the right hand side of the hovered icon (Diagram #2), all you need to do is define the scale with using a CSS adjacent-sibling selector, E + F (an F element immediately preceded by an E element).

For the icon at the left (Diagram #3), ss I mentioned earlier, there is no css to get the *previous* sibling, so I need to rely on JavaScript.  
I used the DOM node interface, `previousElementSibling` to access the sibling node. `previousElementSibling` should be supported by Webkit, Opera and Firefox.

Basically what I am doing here is that get the mouseovered object (should be an img element), find the parent li element (the immediate parent should be an a-alement, not a li, so get a&#8217;s parent! Check the HTML code again!), find the previous sibling li, then give a classname &#8220;prev&#8221; so I can apply the style.  
Don&#8217;t forget to remove the class name as mouseout, otherwise the icon stays large. 

```javascript
function addPrevClass (e) {
  var target = e.target;
    if(target.getAttribute('src')) { // check if it is img
      var li = target.parentNode.parentNode;
      var prevLi = li.previousElementSibling;
      if(prevLi) {
        prevLi.className = 'prev';
      }
	
      target.addEventListener('mouseout', function() { 
        prevLi.removeAttribute('class');
      }, false);
  }
}
if (window.addEventListener) {
  document.getElementById("dock").addEventListener('mouseover', addPrevClass, false);
}
```

For more details with the fancy CSS3 effects (e.g. the gradient and 3D-transform to create the &#8220;base&#8221; of the dock), please see the source code of the <a href="https://dl.dropboxusercontent.com/u/1330446/demo/dock/dock.html" target="_blank">demo page!</a>

 [1]: /assets/images/wp-content/misc/dock-screenshot.jpg