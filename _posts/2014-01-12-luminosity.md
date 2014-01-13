---
title: Responsive UI with Luminosity Level
author: Tomomi Imura
layout: post
categories:
  - Dev
  - HTML5
  - Javascript
  - CSS
  - mobile
  - rwd 
  - firefox
  - ui/ux
  - design
---

Happy new year!

I wonder how the year 2014 will be in terms of the web standards and HTML5, as the first biggest news of the year from W3C was the MPAA joining the W3C as a member and the controversy on DRM has heated up again.

My first blog of the year is not going to be about DRM, but I write a topic on responsive design with ambient light level, which I cover a little bit at SF HTML5 meetup last November, where I received some oohs and aahs so I want to write about it more here.

## Screen readability under sunlight

My Lumia phone comes with the awesome sunlight readability enhancement feature. It detects the light levels in my environment and adjust the screen accordingly. When I get outside under the sun from indoor, the luminance of the screen increases, so I can still read my screen just fine. On the other hand, my another phone, an Android device becomes totally useless under such brightness.
So it doesn't matter how the web sites are made "Mobile first" and how "responsive" they claimed to be, I just can't read anything. I wish all other phones work just like Lumia.

Meanwhile, sometimes last year, on W3C CSS mailing list, I learned the `luminosity` media feature was coming to the [CSS Media Queries 4][mq4], and I was excited. Yes, besides screen resolutions, orientations, pixel density and such, we will be able to make web responsive with the environmetal light level too, once the spec is implemented in browsers!

Awesome. But when will it happen?


## Ambient Light Events API

So there is no way for us to adjust the readability with light level using CSS in this moment, however, we already have the [Ambient Light Events][ambient].
This is a part of the HTML5 [Device APIs][dap], which make browsers to interact with devices services. Ambient Light Events API allows to access the light/photo censor, using simple JavaScript.

Now I can use the API to emulate the yet-to-come CSS Level 4 Media-queires to make a web responsive to the light level!

### Devicelight events

A browser fires the `DeviceLightEvent` event when the light sensor of a device detects a light level change. You can capture the event by using the `devicelight` event handler event type.

Its property, `value` returns the level of the light in *lux* unit.

```javascript
window.addEventListener('devicelight', function(event) {
  console.log(event.value + 'lux');
});
```


### Making web responsive to light

I have made a super simple demo.

What I did is basically changing the UI, depending on the light level in the device environment for better readability. 

- Default: display in black text and light gray background
- Under bright light: black text and white background
- In darkness: white text and dark background


```javascript
window.addEventListener('devicelight', function(e) {
  var lux = e.value;
 
  if(lux < 50) { // dim
    document.body.className = 'dim';
  }
  if(lux >= 50 && lux <= 1000) {
    document.body.className = 'normal';
  }
  if(lux > 1000)  { // bright
    document.body.className = 'bright';
  } 
});
```

```css

body,
body.normal {
  background-color: #ddd;
  color: #111;
}
body.dim {
  background-color: #444;
  color: #fff;
}
body.bright {
  background-color: #fff;
  color: #333;
}
```

Here's the video showing the demo in action.

<iframe src="//player.vimeo.com/video/79466285" width="500" height="280" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

### Browser supports and Devices


The source code is on [CodePen][codepen].

Most of you will probably noticed the message that says *"AmbientLightEvent is not supported."* on the browser you are currently looking at.
Sadly, this API is currently only supported by [**Firefox 22+**][ff], and the hardware needs to be equipped with a sensor to detect light. In my demo, I am using Firefox on **Nexus 7**.

The actual values returned from the event seem to be varied depending on the devices (Android and FirefoxOS) I tested. Probably the sensor's sensitivity are different.

![MotoG and Keon](/assets/images/articles/2014/01/luminosity-devices.jpg "MotoG and Keon")

The photo shows that the Motolora G and Keon FirefoxOS devices show different values under the same dim room light. (6 lux vs. 61 lux!)

## CSS Media Queries Level 4 Luminosity

OK, let's go back to the original topic, Luminosity media-queries.
Currently, the [specification][mq4] is under editor's draft, which means that the spec is still in really early stage and unstable. It will take a while to see it in action on browsers.

Once this is supported, the JavaScript sample can be re-written only with CSS:

```css
@media screen and (luminosity: normal) {
  body {background-color: #ddd; color: #111;}
}
@media screen and (luminosity: dim) {
  body {background-color: #444; color: #fff;}
}
@media screen and (luminosity: washed) {
  body {background-color: #fff; color: #333;}
}

```

We can simply use `luminosity` media feature to query the light level, just like any other media features we are already used to write to create responsive web.

Now, we have more things to worry when thinking of RWD ;-)


[mq4]: http://dev.w3.org/csswg/mediaqueries4/#luminosity
[ambient]: http://www.w3.org/TR/ambient-light/
[dap]: http://www.w3.org/2009/dap/
[codepen]: http://codepen.io/girliemac/pen/pvmBs
[ff]: https://developer.mozilla.org/en-US/docs/Web/API/DeviceLightEvent
