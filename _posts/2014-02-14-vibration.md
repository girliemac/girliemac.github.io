---
title: "Vibration API Use Case: Form Validation"	
author: Tomomi Imura
layout: post
categories:
  - Dev
  - HTML5
  - Javascript
  - CSS
  - mobile
  - firefox
  - ui/ux
---

## Vibration API Last Call

The [Device API Working Group][1] has published a third Last Call working draft of the [Vibration API][2], and since the API is highly relevant to mobile devices, we have been discussing about it on W3C's [Web and Mobile Interest Group][3] (aka *WebMob*).

## Use cases

There has been some (dirty) jokes about the use cases in past, and recently Terrence Eden came up with funny use cases that actually may be somehow useful([*Malicious Use of the HTML5 Vibrate API*][4]).

But seriuously, what can be good use cases for this API for everyday web expeiences besides gaming? 
I was even thinking that this API can be more harmful than useful when there is no UI indication (or permission setting like Geolocation) associated with it, and confuses users if developers abuse the API.

Then, [Michael van Ouwerkerk suggested][mailinglist] form validation. He mentioned on the mailing list - "Especially on mobile devices, with the software keyboard being displayed, it is easy to miss visual form validation messages. Some additional tactile feedback is an easily learned signal."

Ah, finally there is a good use case scenario!


## Demo

So I quickly put things up together to see how it works in a real life scenario. I used my old HTML5 form validation demo I wrote for Nokia Code Blog (Bummer, it has been deleted while cleaning up the Nokia assets for Microsoft's partial aquisition. But I have the copy on [my blog][5] in 2012!)

Here is the demo in action. **Turn the volume all way up** so you can hear my phone buzzes:

<iframe src="//player.vimeo.com/video/86735842" width="500" height="280" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

You can [try it][6] by yourself on latest Firefox browser on Adnroid. (This demo fails on FF18 on FirefoxOS. Probably because the constraint validation doesn't work? I need to look into it!)

Basically, what it does is that when a user tries to submit the form while the `required` field is left empty, or the entered text does not match the requirement (In this case, the character entered do not match the pattern for Twitter username, where some special chars are not allowed.), the phone buzzes as a feedback.

### Code

```html
<form>    
   <input id="username" type="text" pattern="^[A-Za-z0-9_]{1,15}$" required> 
   <input type="submit" value="Submit"> 
</form> 
```

The credit for the pattern matching for the Twitter username goes to [HTML5Pattern][7] :-)

```javascript
navigator.vibrate = navigator.vibrate || navigator.mozVibrate;
	
document.getElementById('username').addEventListener('invalid', function(e) {
    e.target.setCustomValidity("Enter a valid username, dumbass!");
    navigator.vibrate([100, 50, 100]);
}, false);
```

In the demo, when the `invalid` event is fired, the sequience pattern makes the device to vibrate shortly twice - for 100 ms, be still for 50 ms, and then vibrate for 100 ms.


I hope to see more use cases for the API.


[1]: http://www.w3.org/2009/dap/
[2]: http://www.w3.org/TR/2014/WD-vibration-20140211/
[3]: http://www.w3.org/Mobile/IG/
[4]: http://shkspr.mobi/blog/2014/01/malicious-use-of-the-html5-vibrate-api/
[5]: http://girliemac.com/blog/2012/11/21/html5-form-validation/
[6]: https://dl.dropboxusercontent.com/u/1330446/demo/vibration.html
[7]: http://html5pattern.com
[mailinglist]: http://lists.w3.org/Archives/Public/public-web-mobile/2014Feb/0022.html