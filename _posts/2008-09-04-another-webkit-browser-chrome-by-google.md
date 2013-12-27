---
title: 'Another WebKit browser &#8211; Chrome by Google'
author: Tomomi Imura
layout: post
permalink: /blog/2008/09/04/another-webkit-browser-chrome-by-google/
categories:
  - CSS
  - Dev
  - Google
  - WebKit
---
So Google has just released Chrome browser, which Mac user still have to wait for its Mac release. I tried to install on VMWare to see how it is like.

It is a WebKit-based with a brand-new V8 JavaScript engine, which supposed to be much faster than existing JavaScript interpreters. Also, Chrome currently supports almost as much CSS3 that Safari 3 supports. 

Actually I haven’t really tested yet (cuz my main machine is a Mac of course, and my Vaio is dead now), but as long as I quickly took a look at the test page I made, some are not working quite right &#8211; e.g. `text-shadow` <del datetime="2009-01-23T20:38:06+00:00">and <code>box-shadow</code></del> (Correction: box shadow works with webkit extension, as `-webkit-box-shadow`). Animation and Transform CSS work as expected. (Just like Safari 3.2) 

So how about mobile? Current Android browser already uses WebKit engine, so Chrome Mobile will be the future browser for Android?

Yes. <a href="http://news.cnet.com/8301-1001_3-10031318-92.html?part=rss&subj=news&tag=2547-1_3-0-20" target="_blank">According to Sergey Brin</a>, Chrome is going to be available for the platform later.

![Chrome on Android][1]  
(This is not a real Android UI. I just photoshopped.)

 [1]: /assets/images/wp-content/misc/chromeAndroid.jpg