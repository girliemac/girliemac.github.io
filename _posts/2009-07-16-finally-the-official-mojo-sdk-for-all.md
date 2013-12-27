---
title: Finally, the official Mojo SDK for all!
author: Tomomi Imura
layout: post
permalink: /blog/2009/07/16/finally-the-official-mojo-sdk-for-all/
categories:
  - Dev
  - Palm
  - SDK
  - WebKit
---
![][1]

After I was rejected for the early access then struggled with the &#8220;leaked&#8221; version of Palm Mojo SDK without a documentation, today Palm finally made <a href="http://developer.palm.com/" target="_blank">the official SDK available</a> for all!!! 

I haven&#8217;t playing around with it long enough to blog much about it, so I just post my &#8220;cheat sheet&#8221; that I keep on Stickies. 

## Emulator Key for Mac

*   **Esc** &#8211; acts as &#8220;Back&#8221;
*   **Left / Right arrows** &#8211; Switch between applications

## Emulator Navigation

&#8220;Host&#8221; = Right Ctrl in Virtual Box

*   Host + F &#8211; Toggle full screen view on/off 
*   Host + N &#8211; Display session info 
*   Host + S &#8211; Take a snapshot (will be placed the Snapshot tab of VirtualBox) 
*   Host + Q &#8211; Close the emulator </ul> 
                
## Commands
                
#### Create a package (.ipk file)

```bash
$ cd palm-package myapp
```

#### Install the .ipk file on emulator

```bash
$ palm-install com.yourdomain.app.myapp_1.0.0_all.ipk
```

#### Launch the app on emulator

```bash
$ palm-launch com.yourdomain.app.myapp
```

#### Launch the inspector with the app

```bash
$ palm-launch -i  com.yourdomain.app.myapp
```

Then, open Palm Inspector app (comes with SDK) from your Application by double-clicking the icon. This should open the Safari inspector.

 [1]: /assets/images/wp-content/misc/mojo_sdk.png