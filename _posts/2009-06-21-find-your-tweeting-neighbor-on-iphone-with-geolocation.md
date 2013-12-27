---
title: Find Your Tweeting Neighbor on iPhone with GeoLocation
author: Tomomi Imura
layout: post
permalink: /blog/2009/06/21/find-your-tweeting-neighbor-on-iphone-with-geolocation/
categories:
  - Dev
  - Firefox
  - iPhone
  - Sandbox
  - Twitter
  - WebKit
---
![screenshot][1]

iPhone OS 3.0 is now available, and developers can take advantage of the newly introduced **geolocation** feature in Safari browser.

To try it out quickly, I used Twitter Search API again to create a tiny test app called, <a href="http://girliemac.com/geo" target="_blank" />NeighborTweet</a>, which enable you to find out who are tweeting in your neighborhood. Basically, what it does is that obtain your location, and pass the latitude and longitude data to Twitter search and display the result tweets.

Try it out on your iPhone with:  
Short URL <a href="http://girliemac.com/geo" target="_blank" />http://bit.ly/K0ZaE</a>  
or  
<a href=http://qrcode.kaywa.com/img.php?s=8&#038;d=http%3A%2F%2Fgirliemac.com%2Fgeo">This QR Code</a> with scanning app like BeeTagg.

If you are interested in learning more on Twitter search API and geocode, please read <a href="http://apiwiki.twitter.com/Twitter-Search-API-Method%3A-search" target="_blank">Twitter Wiki</a>.

OK, now here&#8217;s the code.  
To find out your location with Geolocation class is simple &#8211; you just call `getCurrentPosition()` method. This initiates an asynchronous request to detect the user&#8217;s position.

```javascript
navigator.geolocation.getCurrentPosition(someFunction)
```

Get latitude and longitude, by using `coords` instance:

```javascript
latitude = position.coords.latitude;
longitude = position.coords.longitude;
```

Here&#8217;s an actual code I used to create the sample app:

```javascript
if (navigator.geolocation) {  
  navigator.geolocation.getCurrentPosition(function(position) {  
    callback(position.coords.latitude, position.coords.longitude);  
  });
} else {  
  alert("Geolocation services are not supported by your browser.");  
} 

function callback(lat,lon){
  // twitter search json-p callback
  var geocode = "&#038;geocode=" + lat + "%2C" + lon + "%2C1mi"; 
  var fullUrl = url + geocode;   
  ...
}
var url = "http://search.twitter.com/search.json?callback=getTweets";

function getTweets (json) {
  // display json data
  ...
}
```

## References

#### Geolocation References:

*   <a href="http://developer.apple.com/safari/library/documentation/AppleApplications/Reference/SafariWebContent/GettingGeographicalLocations/GettingGeographicalLocations.html" target="_blank">Safari Reference Library &#8211; Getting Geographic Locations</a> &#8211; Apple Developer Connection
*   <a href="https://developer.mozilla.org/En/Using_geolocation" target="_blank">Using geolocation</a> &#8211; Mozilla Developer Center
*   <a href="http://www.w3.org/TR/geolocation-API/" target="_blank">Geolocation API Specification</a> &#8211; W3C Working Draft

#### More References:

*   <a href="http://apiwiki.twitter.com/Twitter-Search-API-Method%3A-search" target="_blank">Twitter Search API Wiki</a>
*   <a href="http://bob.pythonmac.org/archives/2005/12/05/remote-json-jsonp/" target="_blank">Remote JSON &#8211; JSONP</a>

 [1]: /assets/images/wp-content/misc/neighbortweet.png