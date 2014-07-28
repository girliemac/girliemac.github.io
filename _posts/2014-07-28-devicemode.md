---
title: Responsive Web Made Easier with Chrome DevTools Device Mode
author: Tomomi Imura
layout: post
categories:
  - rwd
  - mobile
  - Chrome  
---

Note: I originally wrote this article for [HTML5Experts.jp][html5j] in Japanese, as a part of their Google I/O special editions. This blog post is more of the abridged version of the original, which uses more actual quotes (translated) from Google I/O.

---

## Device Mode

Last month at Google I/O, [Paul Bakaus][paulb] introduced a set of brand-new (still experimental) tools, called *Device Mode* for Chrome DevTools. Currently, this feature is only available on Chrome Canary (v38 and newer). 

The Device Mode comes with presets of device information including width, height, and DPI from popular devices like Nexus 5 and Samsung Galaxy series, and makes responsively designed web development easy for us. 

## Media-Queries Tool

Once you open up DevTools in Chrome Canary, you see a little device icon on top. By clicking it, the regular webpage view becomes the device mode. Here you can resize the window, or choose one of the devices from a dropdown menu. If you choose a device with a large resolution, you can make the screen shrinks to fit in the display pane too. Also, switching its orientaion by swapping the width and height values by clicking the toggle button.


![devicemode01](/assets/images/articles/2014/07/devtools-device-mode-1.gif "Device Mode")

What I found more useful is the Media-queries tool. Clicking the icon at the left side of the device presets, you get the visual representations of the media-queries used for the page. Select one of these from the UI and right-click it displays the path of the CSS file. Click the file to inspect the source code!

![devicemode02](/assets/images/articles/2014/07/devtools-device-mode-2.gif "Media-queries")

Apparently, with another new feature called Workspace, you can edit the media-queries on DevTools, and the changes reflect to the local file systems on the fly.

## Connectivity

The new tool comes with the network emulation presets as well. From the dropdown, you can pick mobile networks like 3G and EDGE to emulate the connectivity, and make performance testing easier.

![devicemode03](/assets/images/articles/2014/07/devtools-device-mode-3.gif "Network")

## Remote Debugging with Screencast

The new screencasting feature comes with Carary build 38.0.2101.0 and newer.

To use the experimental features, you need to enable the *DevTools Experiments* from `chrome://flags/#enable-devtools-experiments`. Then open the DevTools and click the gear icon to manually turn on the screencast feature.

Also, you need to turn on USB Debug mode on your Android device.

Once you connect a deivice to your desktop with a USB cable, you should see an little device icon with "1", which indicates the number of devices connected. Then click "Try Here" button to open a screencast window.

![screencast](/assets/images/articles/2014/07/devtools-device-mode-screencast.jpg "Screencast")

You should be able to navigate the page from both device and the screencat.

Clicking "Layers" tab gives you a visualized DOM layers to measure rendering and painting. You can pinpoint where painting jankiness occurs with another new feature, Paint Profiler too.

![screencast](/assets/images/articles/2014/07/devtools-device-mode-screencast.gif "Screencast")

## Takeaway

Here's a list of the DevTools new features for mobile development:

Responsive Layouts

- Rich reprresentsation of media queries
- Style filtering
- Media-queries editting
- Inline emulation

Rich Emulaton

- Device Presets for most popular devices
- Rich viewport emulation
- Sensor emulation (touch, geoloc, accelerometer)
- Network throttling and offline

Remote Debugging

- Plug and play
- Existing but more powerful features
- Screencast
- Port forwarding 

I am pretty exited with the cool new features, and hoping it to be more polished to make available for the stable Chrome release soon. Keep up the great work, Chrome team!


[html5j]:http://html5experts.jp/girlie_mac/8384/[paulb]: http://paulbakaus.com