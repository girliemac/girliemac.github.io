---
title: IndexedDB is finally something
author: Tomomi Imura
layout: post
categories:
  - Dev
  - HTML5
  - Javascript
  - mobile
  - firefox
  - Chrome  
---

![screenshot](/assets/images/articles/2014/07/coremob-camera-idb.png "IndexedDB in Coremob Camera app")
"Woo-hoo, finally!!!" (I should stop being grumpy!) 

This was the first reaction I had when I heard the new on Twitter about Chromium started supporting blob on IndexedDB. And now I know it is official after seeing the [blog post on HTML5 Rocks][html5rocks] by a Chrome developer advocate, also a good friend of mine, Eiji Kitamura.

Why was I so excited? Because I have been waited this for 1.5 years since I started writing **Coremob Camera**. When I started this project, IndexedDB support was super spotty, and I felt Firefox for Android was my only friend who listened to me. (FirefoxOS wasn't quite there yet).

## Coremob Camera

If you have seen me talking at conferences before, you may have heard about Coremob Camera, the open web standards project I was working on, although I failed to thoroughly document it.

[Coremob Camera][coremobcamera] is a web project that mostly I and Tobie Langel worked on for W3C's Core Mobile Community Group (now [Web and Mobile Interest Group][webmob]) to showcase the capability of the web platform, especially on mobile devices. We were hoping to help web developers out there to learn about HTML5 use cases, as well as help improve web browsers.


## The State of IndexedDB

One of the key features we focused as a real-life use case is [IndexedDB][w3c]. The good new was that Internet Explorer 10 supported IndexedDB. The bad news was that Safari had no plan of supporting it, also IndexedDB API was pretty new and unstable at that time the project started. Actually, bad news overwhelmed the good news.

I talked about my agony at **W3Conf** ([video][w3conf]) last year, then bitterly joked about complete lack of support by Apple, and IndexedDB was not ready to use, at **All Your Base Conf** ([video][ayb], Also the slides below).

<script async class="speakerdeck-embed" data-id="bda5d8c019b201318b443620859eaef1" data-ratio="1.6" src="//speakerdeck.com/assets/embed.js"></script>


My biggest tormenters were:

- No adequate browser support (missing in Safari, Android stock, Presto-Opera)
- Vendor prefix
- Chaotic coexistence of deprecated specs and new specs on supported browsers 
   - `setVersion()` vs. `onupgradeneeded`
   - `IDBTransaction.READ_WRITE` vs. `"readwrite"`
   - Chrome uses string for version instead of number
- No blob support (Only Firefox supported)
   
The specifications have been modified multiple times. For example with Firefox's case, the basic iDB support started in version 4, `setVersion()` was deprecated at ver 10, and transaction mode has been switched to string from constant since 13. For mobile support (Firefox's earliest Android support was ver 16-ish), I could just stick with the latest specs; however, Chrome came to the iDB space later with slightly older specifications.

Because I never knew which specifications and features were supported on what browsers, also annoying issue such as Chrome's silent failure when trying to store blobs, I had to use a bunch of feature detections and  `try` / `catch` for fail-proof for the buggy Chrome 18 and Blackberry 10 (which was less PITA than Chrome).

### Chrome's Fashionably Late Mobile Debut

It's 2014 now, and this year's Google I/O was all about Android-
It is almost unbelievable for you when I say Chrome was fashionably late to the Android party. But the truth is, Chrome was not even available until late 2012, at version 18.

Despite the fact that Google ships Chrome quite often (along with Beta, Dev, and Canary nightly release) for desktop, I never could have any updates for my Nexus 4, during the time of the Coremob Camera development. After I patiently waited, good news came to me finally in March 2013. It was Chrome 25! Yes, there was a big gap between 18 and 25.

Ever since, Google constantly releases Beta version for Android as well.

### Awesome Chrome Dev Tools

Besides the lack of blob supports, I have been always a big fan of Chrome's *DevTools*. As well as DOM and CSS debugging, and monitoring performance, you can inspect web storages too. Visualizing the contents in your IndexedDB is easy with Chrome.

![devtools](/assets/images/articles/2014/07/devtools.gif "Inspect iDB on Chrome DevTools")


## To Blob or Not to Blob

Blob support was somehow important for me, because Coremob Camera is all about photos. In the app scenario, the user flow is as follows:

1. Take a picture via **HTML Media Capture**
2. Use `FileReader()` to return the picture as an object
3. `drawImage()` to draw the image object in canvas
4. `getImageData()` to get an ImageData object containing a copy of the pixel data, then alter the pixels
5. Store the **blob** locally with **IndexedDB**
6. Upload the final photo with **XHR2** over **CORS**

(Whoa, I successfully gave you a bunch of HTML5 use cases in a single web app, right!?)

For the step 5, since only Firefox was supporting blob in IndexedDB, I had to use Base64 data URL strings for unsupported browsers. Me, grumpy grumpy.

## Good news and more good news

So, I felt like it has been a long time (a long InterWeb years) since I started using IndexedDB experimentally.

![WWDC](/assets/images/articles/2014/07/wwdc.png "Safari 8")

At this year's WWDC, Apple announced new features coming to Safari 8, including yes, IndexedDB support! 

And I am delighted with the arrival of Chrome 37, which has blob support for IndexedDB!

IndexedDB is finally something.

![yes](/assets/images/articles/2014/07/cry.png "Finally!")

Note: Currently, Chrome 37 (Dev) is not available on Android yet! Until then, you can try [Coremob Camera][app] on desktop!

## References

- W3C [Indexed Database API][w3c]
- Can I use [IndexedDB?][caniuse]?


[coremobcamera]: https://github.com/coremob/camera/
[webmob]: http://www.w3.org/Mobile/IG/
[html5rocks]: http://updates.html5rocks.com/2014/07/Blob-support-for-IndexedDB-landed-on-Chrome-Dev
[w3c]: http://www.w3.org/TR/IndexedDB/
[caniuse]: http://caniuse.com/indexeddb
[w3conf]: https://www.youtube.com/watch?v=3Afi-v-m_Gc
[ayb]: https://vimeo.com/83837733
[app]: http://coremob.github.io/camera/vanilla/index.html