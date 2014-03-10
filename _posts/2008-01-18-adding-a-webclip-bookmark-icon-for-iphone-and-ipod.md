---
title: Adding a WebClip Bookmark Icon for iPhone and iPod
author: Tomomi Imura
layout: post
permalink: /blog/2008/01/18/adding-a-webclip-bookmark-icon-for-iphone-and-ipod/
categories:
  - Dev
  - iPhone
  - UI/UX
---
 
While MacWorld is held here in San Francisco, I am commuting to Sunnyvale&#8230; At least I am trying to catch up with all these exiting news from Apple. 

One iPhone dev-related announcement caught my attention is a WebClip. -The WebClip is a web bookmark icon that is displayed on start screen on iPhone (and iPod), and looks just like an application launch button. (To make it work, you need to upgrade the firmware to 1.1.3.)

To create a custom icon is as easy as adding a favicon.ico for desktop website.

First, create a 57×57 png image. (Don&#8217;t worry about round-corners and shine.) 

Then do either:  
  
1) Place a PNG image named **apple-touch-icon.png** at the root directory of your web server.  
  
or  
  
2) Add `<link rel="apple-touch-icon" href="/customIcon.png"/>` within the `<head>` element of the page.

Once added to the springboard screen, round-corners and glassy overlay will be added to your icon nicely :-)