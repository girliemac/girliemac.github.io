---
title: Mobile Safari for iPhone 3 includes Geolocation
author: Tomomi Imura
layout: post
permalink: /blog/2009/06/01/mobile-safari-for-iphone-3-includes-geolocation/
categories:
  - Firefox
  - iPhone
  - WebKit
---
Although W3C&#8217;s document, <a href="http://www.w3.org/TR/geolocation-API/" target="_blank">The Geolocation API Specification</a> is still in draft state and not yet finalized, major browsers are working to support this functionality and as we all expected, Mobile Safari is not an exception.

According to <a href="http://blogs.computerworld.com/iphones_safari_browser_to_include_geolocation_0" target="_blank">ComputerWorld blog</a>, the geolocation API has been implemented for the upcoming API. Apparently, Seth of ComputerWorld tried the test webpage, built by Doug Turner for Mozilla on a 3.0B5 iPhone&#8217;s Mobile Safari.  
This screenshot is grabbed from the CompWorld&#8217;s blog.  
![][1] 

Obviously I don&#8217;t have access to the new iPhone so I just tested the test page (<a href="http://people.mozilla.org/~dougt/geo.html" target="_blank">http://people.mozilla.org/~dougt/geo.html</a>) using Geolocation API `watchPosition()` method, on Mozilla 3.5. (And this should works similarly on Fennec too. I wish I could try on an actual device!)

![][2]  
  
![][3]

I am using my old PowerBook G4, with Comcast,. Since this Mac is not equipped with GPS device, Firefox gathers information about nearby wireless access points and computer’s IP address.

Nice! I can&#8217;t wait to see this working on iPhone!  
Especially, NextMuni.com with location enabled, that tells me where I am and where the nearest bus stop!

 [1]: /assets/images/wp-content/misc/compWorld_iphone_geo.png
 [2]: /assets/images/wp-content/misc/ff35_geo01.png
 [3]: /assets/images/wp-content/misc/ff35_geo02.png