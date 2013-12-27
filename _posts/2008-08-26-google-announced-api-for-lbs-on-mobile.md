---
title: Google announced API for LBS on Mobile
author: Tomomi Imura
layout: post
permalink: /blog/2008/08/26/google-announced-api-for-lbs-on-mobile/
categories:
  - Dev
  - Google
  - WAP
---
Google launched the Gears Geolocation API for mobile on last week on their <a href="http://google-code-updates.blogspot.com/2008/08/two-new-ways-to-location-enable-your.html" target="_blank">official Goolge code blog</a>, and <a href="http://googlemobile.blogspot.com/2008/08/new-gears-geolocation-api-powers-mobile.html" target="_blank">Mobile Blog</a>, with a screenshot of a sample mobile site, *Rummble* and video demo of *lastminute.com* of UK. 

On mobile devices with Gears installed, Javascript functions grab the cell-ID of nearby cell towers or GPS (if either is available) to improve the postion fix. 

<img src="/assets/images/wp-content/misc/google_lbs.png" align="right" />

The two methods:  
`getCurrentPosition()` makes a single, one-off attempt to get a position fix.  
`watchPosition()` watches the user&#8217;s position over time, and updates the position changes.

Also,  
` lastPosition` get an approximate position fix 

The bad news is that API is available on Internet Explorer, Firefox and IE Mobile (<a href="http://www.google.com/support/mobile/bin/answer.py?answer=105928" target="_blank">selected devices only</a> &#8211; incl. Samsung Blackjack II, HTC Touch Dual, TyTN, Palm Treo750 etc.) and will be available on Android. I was going to try it with S60, until I read the line on the announcement.

The good news is that they are currently implementing the editor&#8217;s draft of the <a href="http://dev.w3.org/geo/api/spec-source.html" target="_blank">W3C Geolocation specification</a> with Microsoft and Mozilla guys.