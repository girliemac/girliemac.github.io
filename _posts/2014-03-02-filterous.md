---
title: "Filtrous.js Photo Manipulation Library"	
author: Tomomi Imura
layout: post
categories:
  - Dev
  - HTML5
  - Javascript
  - mobile
  - firefox
---

![Filtrous](/assets/images/articles/2014/03/filtrous.jpg "Filtrous")

[Filtrous.js][filtrous] is a photo manipulation library in JavaScript that applies filters to photos à la Instagram on browser. 

I originally wrote this photo manipulation tool as a part of *CoreMob Camera* last year, and now I just released it as a separated library.


### Camera App running on a browser

<img src="/assets/images/articles/2014/03/coremobcamera.jpg" width="350" alt="CoreMob Camera" align="right">


Last year was incredibly busy for me, and I totally failed to propertly document about this web app, although I promissed to write up on a separated blog.

I originally started writing this app in the end of 2012, with help of Tobie Langel, Dominique Hazael-Massieux et al. as a side project for [Core Mobile Web Platform W3C Community Group][coremob] (which is now closed and reborn as [Web and Mobile Interest Group][webmob]). 

The web app (also, I have created a hybrid app with PhoneGap) was called [CoreMob Camera][camera], which allows you to take a snapshot directly from a browser, and apply filters to the photo, save onto the browser, also send to server. The whole purpose was to showcase the capabilities of the Web platform, showing developers HTML5 use cases on mobile, and help improve browsers by showing bugs, missing features etc. to browser vendors. 

If you are curious, [try the app on mobile browser][cameraapp]. This fails on some browsers, and the vendors are acknowledged.

I also talked about this app and the technology on several conferences, including [W3C Conf][w3conf], so watch it if you are interested! (Watch my talk on [YouTube][video]). Also, I was demoing this web app at Mobile World Congress 2013. See [my interview][interview] on W3C Blog ;-)


## Filtrous.js - Tweak Pixels with Canvas

Anyway, *Filtrous.js* take pixel data from a photo that you want to give filter effects, and maniplute its pixels using the `canvas` element. The finished photo can be displayed as canvas, or as downloadable image formats such as jpeg, png, or webp for Chrome.

This is how the photo manipulation works-

- First a `<canvas>` is defined and import an photo into the canvas by using `drawImage()` method to draw the image object. 
- Then, use `getImageData()` method to obtain an `ImageData` object containing a copy of the pixel data for a context.
- Then "applying filter" by tweaking the pixel data, which I will talk a bit more on the next slide.
- Finally, using `putImageData()` method, paint pixel data back into a context.

The calculation of tweaking pixels is actually done on each canvas pixel by looping through one by one, so foe example, if your photo dimension is 100 x 100, you need to interate the operation for 10,000 times, and this can be slow on mobile. Well, at least I thought so last year, but mobile hardware and browsers have improved like crazy and I am surprised how quickly it can be on mobile done now, even with my "low-cost" Moto G device.


### Usage 

Using Filtrous is easy. See this [Demo][demo] too.


```html
<img id="myPhoto" scr="cat.jpg">

```

```javascript
var myPhoto = document.getElementById('myPhoto');
var f = new Filterous(myPhoto, 'jpeg'); // output: jpeg, png, webp. default is canvas

```

The image on top of this blog shows examples of combination of "beightness" and "rgbAdjust" filters (center), and grayscale (right).

The effect in the middle can be achieved by applying two filters:
 
```javascript
f.filterImage('rgbAdjust', [1, 1.2, 1.4]);
f.filterImage('brightness', 10);
f.render();
```


Also, I have made an extra JS file that you can import, so you can use the named preset effects such as "nostalgia" (slightly sepea tone) and "rockstar" (with starry overlay) that you see in the demo.

If you would like to use *Filtrous*, see my [github][filtrous] page for more info :-)


## Why not CSS3?

Multiple people have asked me why I used `canvas` while the CSS3 Filter effects has been adopted by WebKit and Blink browsers.
I love the ease of using the CSS3 filters and wrote a [blog]({% post_url 2011-12-21-quick-fun-css3-filter-effects%}) about it too. However, unlike the pixel manipulation in canvas, the CSS filter is just a visual representation and it does not actually alter the physical property of the photos. When you download the filtered photo, you still get the unfiltered original image.

## Links

- [Filterous.js on Github][filtrous]
- [Filterous.js Demo][demo]
- [CoreMob Camera][camera]


[github]: https://github.com/girliemac/
[filtrous]: https://github.com/girliemac/Filterous
[coremob]: https://github.com/coremob
[webmob]: https://github.com/w3c-webmob
[camera]: https://github.com/coremob/camera
[cameraapp]: http://coremob.github.io/camera/vanilla/index.html
[w3conf]: http://www.w3.org/conf/2013sf/
[video]: https://www.youtube.com/watch?v=3Afi-v-m_Gc
[interview]: http://www.w3.org/blog/2013/04/interview-demonstrating-web-ap/
[demo]: http://girliemac.com/Filterous/demo/
