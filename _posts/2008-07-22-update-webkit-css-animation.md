---
title: 'Update: WebKit CSS Animation'
author: Tomomi Imura
layout: post
permalink: /blog/2008/07/22/update-webkit-css-animation/
categories:
  - CSS
  - Dev
  - iPhone
  - Sandbox
  - WebKit
---
Regarding to the bug on CSS animation I mentioned on [last blog entry][1], I got a reply from an Apple developer (Quick!) 

The issue:  
CSS animation doesn&#8217;t work with `onclick="this.className='newClassName'` anymore on the latest WebKit nightly build 

I filed the bug on WebKit Bugzilla, and got the answer already. See <a href="https://bugs.webkit.org/show_bug.cgi?id=20132" target="_blank">the ticket</a>.

Basically, this bug was closed (invalid) because they have decided to change the animation implementaion, from &#8220;source transition&#8221; model to &#8220;destination  
transition&#8221; model.  
(<a href="https://bugs.webkit.org/show_bug.cgi?id=20132#c1" target="_blank">Read</a> the whole explanation)

Stay tuned for the new documentation from WebKit or Apple!

<a style="href="/blog/2008/07/23/more-update-on-css-animation/">UPDATE / CORRECTION (July 23, 08) &#8211; please see &#8220;More Update on CSS Animation&#8221;</a>


 [1]: http://girliemac.com/blog/2008/07/19/webkit-css-animation-examples/