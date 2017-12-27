---
title: Filterous 2 Photo Manipulation Library is Released!
author: Tomomi Imura
layout: post
description: an open-source Instagram-like image manipulation library for Javascript and node.js
images:
  - /assets/images/articles/2017/02/filterous-2.png
categories:
  - dev
  - javascript
  - node.js  
  - images manipulation
  - instagram
---

![filterous-2](/assets/images/articles/2017/02/filterous-2.png)

I recently released **Filterous 2**, an open-source Instagram-like image manipulation library for Javascript and node.js on [npm](https://www.npmjs.com/package/filterous).

This is a revamped version of Filterous, which was written for JavaScript for browser about 4 years ago, and this version works on both Node.js and browser, and comes with pre-defined Instagram-like filters (with the same filter names and very similar effects).

To see how it works, check out the [browser demo](https://girliemac.github.io/filterous-2/demo-browser)!

This demo does not reply on the server, and created solely with front-end JavaScript (and it is vanilla) and browser version of Filterous 2.

## Story Behind the Project

Between 2012 and 2014, I was a member of W3C's Core Mobile Community Group. To demonstrate the HTML5 APIs for mobile phones, I have written the demo called [Coremob Camera](https://github.com/coremob/camera), and show this at the W3C booth at Mobile World Congress in Barcelona ([Interview](https://www.w3.org/blog/2013/04/interview-demonstrating-web-ap/)) in 2013, and talked about the technologies behind at W3C Conference in San Francisco ([My talk on YouTube](https://www.youtube.com/watch?v=3Afi-v-m_Gc)).

Basically the app was like a web app version of Instagram (which, we withheld from  using the name for the legal reason.)- you take a picture from the mobile phone camera, and apply a filter to give the glamorous finish. To add a "filter" feature, I wrote some code to manipulate the original jpeg image, and later, I separated the code out of the whole app to open-sourced it as an independent library.

Four years has passed, and now I decided to make it for node.js, then used [Browerify](http://browserify.org/) to export it for browser use.

## How It Manipluate Images

Filterous takes an image into a `canvas` to manipulate the pixels of the image. Unlike the CSS filters that alters how the image appearance only on browsers, the JavaScript library actually alters the pixel color values. So you can actually download the modified image.

The `CanvasRenderingContext.getImageData()` method of the Canvas API returns an `ImageData` object representing the underlying pixel data of the canvas, and the `data` property of `pixelData` stores the color info of an each pixel in the canvas. (The diagram below shows a canvas size of only 9x9 pixel to make it simple).

Each pixel in the data array consists of 4 bytes values- red, green, blue, and alpha channel, and each of the R (red), G (green), B (blue) and A (alpha transparency) values can take values between 0 and 255.



![canvas image manipulation](https://github.com/girliemac/filterous-2/blob/master/images/canvas-pixels.png?raw=true)

I referenced numerous sources (credited them in my source code) for the algorithms to alter a color image to grayscale, brighten, saturate, etc. and I used the combinations to give the Instagram-like predefined filters. I probably spent most of my time mimicking the entire set of the filter they offer!

The source code and documentation are available on [GitHub](https://github.com/girliemac/filterous-2). If you'd like to file bugs or contribute, please feel free to send me issue and pull requests!
