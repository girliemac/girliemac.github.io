---
title: Creating Non-disruptive Notifications with HTML5
author: Tomomi Imura
layout: post
permalink: /blog/2012/03/29/creating-non-disruptive-notifications-with-html5/
topsy_short_url:
  - http://is.gd/7wfyFL
  - http://is.gd/7wfyFL
dsq_thread_id:
  - 2067961134
categories:
  - HTML5
  - JavaScript
  - Palm
  - WebKit
---
<img src="/assets/images/wp-content/uploads/2012/03/notifications.png" alt="web notifications" title="notifications" class="aligncenter" />

<p style="color:red">Update: The API I used for this article has been <strong>deprecated</strong> by W3C, and the example code no longer works on the latest browser. I have updated the code with using the new specification so please take a look at <a href="https://github.com/girliemac/html5-notifications-webOS-style">my github repo</a>.
<br><br>
Thanks!</p>

---

The **HTML5 Web Notifications API** (now available on Chrome) allows you to display the Growl-like notification windows outside of the web browser window. Unlike the alert dialog, the notification windows do not disrupt a user&#8217;s action, or requires extra user interactions.

Using the API is quite simple, so I tried to replicate the infamous webOS notification system in HTML5. (In case you are not familiar with webOS UI and UX, see it on <a href="http://www.youtube.com/watch?v=G8tFODkacak" target="_blank">YouTube</a>). 

Live demo: <a href="http://girliemac.github.com/html5-notifications-webOS-style" target="_blank">http://girliemac.github.com/html5-notifications-webOS-style</a>

## Basic Notifications

First, check if the browser supports the API, by looking for the Notifications property.

```javascript
if (window.webkitNotifications)
```

Apparently, it is only supported by WebKit-based browser (well, Chrome, so far) so you need to add the vender prefix, instead of just `webkitNotifications`.

Next, your script needs to requests the user agent to ask a user for permission to show notifications. If you are already familiar with the *geolocation* API, you have seen the &#8220;Info bar&#8221; on top of the browser.

![permission bar][1]

To request the permission by `requestPermission()`, you must invoke some event from a user, such as mouse click. See the example below:

```javascript
document.getElementById('#someButton').addEventListener('click', function() {
  // check if a permission is set allowed
  if (window.webkitNotifications.checkPermission() == 0) { // Allowed
    // do show the notifications
  } else {
    // request a user permission
    window.webkitNotifications.requestPermission();
  }
}, false);
```

There are two ways to create the notifications &#8211; plain text or html.

1. Plain text- use `createNotification` function that takes three optional params, icon image, title, and text:

```javascript
var notification = window.Notifications.createNotification(
  'avatar.png', 
  'New tweet from @girlie_mac', 
  'OMG, a glass of water! http://instagr.am/p/...'
);
```

2. HTML &#8211; use `createHTMLNotification` to include an external html file:

```javascript
var notification = window.webkitNotifications.createHTMLNotification('tweet.html');
```

To show the notification:

```javascript
notification.show();
```

Also, you can use the `cancel` method to close the notifications if you wish. This example below let the notification close by itself 5 second after it is displayed:

```javascript
notification.ondisplay = function(event) {
  setTimeout(function() {
    event.currentTarget.cancel();
    }, 5000);
}
```

Besides the `ondisplay`, other event handlers available are:  
`onclick`, `onshow`, `onerror`, and `onclose`.

In my demo, I used the HTML notifications because only the HTML notification style allows you to fully customize the UI with CSS and add some UX with JavaScript.  
To create the webOS-esque &#8220;slide-to-dismiss&#8221; effect, I used jQuery UI&#8217;s draggable and droppable. (I attempted to use the HTML5 drag and Drop, but for some reasons, I could not successfully make my code work within the notification window, although the code does work in a regular window.)  
The source code is on <a href="https://github.com/girliemac/html5-notifications-webOS-style" target="_blank">github</a>.

Hopefully, this API will be available on other browsers. (And Klout will replace the modal dialogs from hell to something more subtle like the web notifications in future. Can you believe once they had me to close seven modals after logging in? This has to be stopped no matter what.)

## References

<a href="<br />
http://dev.w3.org/2006/webapi/WebNotifications/publish/" target="_blank">W3C Draft</a>  
<a href="http://www.chromium.org/developers/design-documents/desktop-notifications/api-specification" target="_blank">Chromium API Specification</a>  
<a href="http://www.html5rocks.com/en/tutorials/notifications/quick/" target="_blank">HTML5 ROCKS</a>

 [1]: /assets/images/wp-content/uploads/2012/03/notifications-permission.png "notifications-permission"