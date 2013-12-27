---
title: 'Quick Demo: CSS3 Fancy Avatar'
author: Tomomi Imura
layout: post
permalink: /blog/2011/02/17/quick-demo-css3-fancy-avatar/
topsy_short_url:
  - http://is.gd/vkqh04
  - http://is.gd/vkqh04
categories:
  - CSS
  - Dev
  - Firefox
  - Opera
  - Sandbox
  - WebKit
tags:
  - css3
---
<img src="/assets/images/wp-content/uploads/2011/02/css3-avatar.png" alt="css3-avatar" title="css3-avatar" width="413" height="106" class="aligncenter size-full wp-image-227" />

Now I started using jsfiddle for code snippets so I can show the code AND the actual results on browsers.

```css
.avatar {
    width: 80px; height: 80px; margin: .5em; display: inline-block;
    
    background-repeat: none; 
    background-size: 100% 100%;
    
    border-radius: 8px;
    
    /* ext needed for Safari5 */
    -webkit-box-shadow: inset -1px -1px 8px #000, inset 2px 3px 1px #fff; 
    /* for recent Webkit, Chrome, FF and Opera */
    box-shadow: inset -1px -1px 8px #000, inset 2px 3px 1px #fff;
}
```


This fancy avatar frame is created pretty easily by using CSS box-shadow inset values.  
Basically, what I did is that giving a div container (with an avatar picture as a background image) an inset shadow to bottom/right, and glare to top/left. Oh and added border-radius for the rounded corners.

This works without the vendor-specific extensions on latest Firefox, Chrome, Webkit Nightly, and Opera. Safari 5 still requires `-webkit` extension to make the box-shadow work.

Really easy and practical!