---
title: 'iCuteOverload Update &#8211; Launch YouTube app'
author: Tomomi Imura
layout: post
permalink: /blog/2007/09/09/icuteoverload-update-launch-youtube-app/
categories:
  - Dev
  - GirlieStuff
  - GirliemacNews
  - iPhone
---
OK, iCuteOverload beta (preview at: girliemac.com/cute on iPhone!) is almost official.

Before handing to Megan, I made another change &#8211; converting YouTube Flash embed (that is not supported by iPhone) to YouTube video link to open in iPhone&#8217;s YouTube app. Thanks to Isao Yagi, who gave me tips to my regex question on php-user list, I could make this work.

Here&#8217;s how the regex code in php looks.

pattern to look for:  

```javascript
$p = ' /<object[\S\s]+?http:\/\/www\.youtube\.com\/v\/([\w\-]+)"[\S\s]+? <\/object>/i ';.<br />
```
 
This look for a html object tag that includes YouTube link, and capture the video ID to re-create a new link.  
As long as I found, the video ID can contain any alpha-numeric char (\w) and hyphen (\-).  
Use /i to make it case-insensitive just in case.

replace string:  

```javascript
$r = ' <a href="http://www.youtube.com/watch?v=\1"><img src="images/watch_youtube.png" alt="watch!" width="200" height="56"/></a>';<br />
``` 
then use preg_replace function to replace the string:  

```javascript
$content = preg_replace($p, $r, $content);
```

I use an image button link to launch YouTube app.  
The captured video ID for Flash is now taken as a query string. This should work fine!

![][1]![][2]

However!!! I just found that NOT all YouTube videos are available for iPhone yet&#8230;  
So when I try the latest CuteOverload entry, I got this sad message, &#8220;Could not load movie&#8221;.

![][3]

According to Apple Support, they will apparently be in sync by the end of the summer.

 [1]: http://farm2.static.flickr.com/1357/1353064060_919600e02f_m.jpg
 [2]: http://farm2.static.flickr.com/1098/1353064106_fd3e0284dd_m.jpg
 [3]: http://farm2.static.flickr.com/1341/1352175377_5210ef8dd4_m.jpg