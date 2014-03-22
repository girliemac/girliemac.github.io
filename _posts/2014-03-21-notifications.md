---
title: Web Notifications Update
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

![screenshot](/assets/images/articles/2014/03/notifications.png "Web notification")

Two years ago, I [wrote a demo and blogged][blog] about then-Chrome-only HTML5 notifications. A while ago, like, 8 Chrome versions ago, I've noticed the demo no longer worked, because the [original specication][oldspec] I was using was deprecated for good.

Around the time, started by Apple first, each browser vendors had its own proprietary notifications API, then last year, they have decided to standardized specification. 

I finally read the [new specifications on W3C][newspec] recently, and rewrote the demo using the standard API.

## New and Simplified Specs

In the original demo, I implemented the notifications in *webOS 3.0-style* UX, which allowed a user to swipe to close the window. (Do you remember HP TouchPad, which was killed soon after the release and gone on fire-sale? I was a UI engineer for the beautiful dead platform.) However, [this v2 demo][demo] no longer supports the swipable notifications UI because the simplified new Web Notifications spcification only allows text and icon, and external HTML (with JS) files are no longer permitted.

## Demo

Check out the new demo: [http://girliemac.com/html5-notifications-webOS-style][demo] (I keep the webOS system config look-and-feel!)

The simplified standard uses `Notification` object to represent each notification. (No `webkit` or `moz` vendor prefixes are required for the supported browsers.)

```javascript
var notification = new Notification('YOLO!');
```

### Request Permission

![screenshot](/assets/images/articles/2014/03/permission.png "Web notification")

Notifications can only be displayed if the user has granted permission. Requesting the user agent to ask a user for permission is done as follows:

```javascript
Notification.requestPermission(callback);
```

This process is done asynchronously, and the callback function is called when the user chooses a permission either `default`, `granted`, or `denied`.

### Displaying Notifications

```javascript
if (Notification.permission === 'granted') {
  var n = new Notification('Meeting', {  
    body: 'March 21 3:30 PM',
	icon: 'calendar.png' 
  });
}
```

![screenshot](/assets/images/articles/2014/03/notification-window.png "Notifications on Chrome")

### Events

`Notification` fires `show` and `close` events during the lifecycle.

To close the notification window after 15 seconds:

```javascript
n.onshow = function() { 
  setTimeout(n.close, 15000);
}
```

## Supported Browsers

- Firefox 22+ (both desktop and mobile)
- Chrome 32+ (Desktop only)
- Safari 6+ on Mac 10.8+ (Damnit, I need to upgrade my Mac to test!)

As long as I tested, the web notifications API is disabled on Chrome for mobile, while Firefox does support the feature (however, it has a UI issue).

## Known Problems

- Chrome for Android does not support the feature
- Firefox on Android does support, however, only one line (the last line) is displayed on the native notification bar on top. No extra UI or window from browser. (tested on Firefox 29. Bug filed #986785.)
- On Chrome (tested on 33), `close()` method does not seem to work. Notification windows fails to close automatically. (Bug filed #355214).

### Firefox on Android

Notifications appear in the native notification bar, one at a time, instead of popup windows from browser.

The problem is that if a notificatin contains more than one lines one messages (when both main text and `body` are set), only the last line (`body`) is displayed, instead of the main title, which I think makes more sense. When the notification bar is expanded by a user, both subject and body text are visible (See the screenshot below).

Also, custom icons aren't shown either. The icon on the notification is always Firefox icon.

![screenshot](/assets/images/articles/2014/03/notifications-moz.png "Notifications from Firefox on Android")

## References

- W3C [Web Notifications][newspec]
- WHATWG [Notifications AP][whatwg]
- Can I use [Web Notifications][caniuse]?
- MDN [Using Web Notifications][mdn]
- Apple Safari Developer Library [Sending Notifications][apple]


[blog]: http://girliemac.com/blog/2012/03/29/creating-non-disruptive-notifications-with-html5/
[oldspec]: http://www.chromium.org/developers/design-documents/desktop-notifications/api-specification
[newspec]: http://www.w3.org/TR/notifications
[demo]: http://girliemac.com/html5-notifications-webOS-style/
[whatwg]: http://notifications.spec.whatwg.org/
[caniuse]: http://caniuse.com/notifications
[mdn]: https://developer.mozilla.org/en-US/docs/WebAPI/Using_Web_Notifications
[apple]: https://developer.apple.com/library/safari/documentation/AppleApplications/Conceptual/SafariJSProgTopics/Articles/SendingNotifications.html 