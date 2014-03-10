---
title: 'Boring Friday night activity &#8211; fixed UI glitch on iCO'
author: Tomomi Imura
layout: post
permalink: /blog/2008/03/08/boring-friday-night-activity-fixed-ui-glitch-on-ico/
categories:
  - Dev
  - GirliemacNews
  - iPhone
---
<img src="/assets/images/wp-content/misc/iCO_webclip.png" style="padding-right: 0.5em" align="left" />I’ve been sick and still recovering from.  
Anyway, my iPhone WebApp, **iCuteOverload** became look uglier after a few firmware updates ago and I had ignored since, but I finally fixed today.

It looks like <a href="http://www.w3.org/TR/css3-ui/#box-sizing">`box-sizing: border-box`</a> stopped woking on the recent WebKit, so I needed to use WebKit’s own declarations by adding `-webkit-` prefex, to adjust the box-model. It was easy fix but didn’t figure out soon enough :-p (maybe because I was watching House M.D. while debugging). Then I looked at the latest [iUi][1] code and well, the fix was already there… I should have just downloaded from beginning.

Oh well.

 [1]: http://code.google.com/p/iui/