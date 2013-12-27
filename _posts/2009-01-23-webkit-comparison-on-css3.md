---
title: WebKit Comparison on CSS3
author: Tomomi Imura
layout: post
permalink: /blog/2009/01/23/webkit-comparison-on-css3/
categories:
  - CSS
  - Dev
  - iPhone
  - Nokia
  - Sandbox
  - WebKit
---
 
Bitstream has launched a new mobile browser called <a href="http://boltbrowser.com/" target="_blank">Bolt</a>, which is a J2ME browser and use WebKit as a rendering engine.

Instead of writing a review on this new WebKit browser, I decided to just do some quick CSS3 test on variety of WebKit browsers!  
If you rather read the review, I recommend <a href="http://wapreview.com/blog/?p=2598" target="_blank">WAP Review</a>. There&#8217;s a very detailed great article on Bolt there.

## WebKit browsers I used

1.  WebKit Nightly for Mac OS X (as a Control)  
    <code class="small">Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_5_4; en-us) AppleWebKit/528.11+ (KHTML, like Gecko) Version/4.0dp1 Safari/526.11.2</code>
2.  iPhone Safari  
    <code class="small">Mozilla/5.0 (iPhone; U; CPU iPhone OS 2_2 like Mac OS X; en-us) AppleWebKit/525.18.1 (KHTML, like Gecko) Version/3.1.1 Mobile/5G77 Safari/525.20</code>
3.  Chrome by Google  
    <code class="small">Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/525.19 (KHTML, like Gecko) Chrome/1.0.154.43 Safari/525.19</code>
4.  HTC Dream Android  
    <code class="small">Mozilla/5.0 (Linux; U; Android 1.0; en-us; dream) AppleWebKit/525.10+ (KHTML, like Gecko) Version/3.0.4 Mobile Safari/523.12.2</code> 
    *   Nokia N95 8GB  
        <code class="small">Mozilla/5.0 (SymbianOS/9.2 U; Series60/3.1 NokiaN95_8GB/10.0.021; Profile/MIDP-2.0 Configuration/CLDC-1.1 ) AppleWebKit/413 (KHTML, like Gecko) Safari/413</code>
    *   Bolt 0.74 on Nokia N95 8GB  
        <code class="small">Mozilla/5.0 (X11; 78; CentOS; US-en) AppleWebKit/527+ (KHTML, like Gecko) Bolt/0.741 Version/3.0 Safari/523.15</code></ol> 
    
## CSS3 Styling I tested
    
```css
.opracity {opacity: .5;}
.textShadow {text-shadow: #777 2px 2px 2px;}
.textShadows2 {text-shadow: rgba(0,0,255, .7) 3px 3px 2px, rgba(255,0,0, .7) -3px -3px 2px;
.ellipsis{text-overflow: ellipsis; width: 200px; overflow: hidden;}
.borderRadius {background-color: #666; color: #fff; width: 200px; padding: 10px; -webkit-border-radius: 10px;}
.boxShodow{-webkit-box-shadow: #000 3px 2px 6px; width: 200px; padding:5px;}
.strokeAndFill{-webkit-text-stroke: 1px green; -webkit-text-fill-color: #ccc; font-size: 2em; }
.borderImg{-webkit-border-image: url(button.gif) 0 13 0 13 stretch stretch; border-width: 0px 13px; padding: 5px 0 7px;}
```
    
## Results
    
**WebKit Nightly** &#8211; This is how everything should look like.

<img src="/assets/images/wp-content/misc/css3/mac_webkit.png" alt="WebKit Nightly" />

**iPhone Safari**

<img src="/assets/images/wp-content/misc/css3/iphone.png" alt="iPhone" />

**Chrome** and **Android Browser** 

<img src="/assets/images/wp-content/misc/css3/chrome.png" alt="Chrome" /><img src="/assets/images/wp-content/misc/css3/android.png" alt="Android" />
 
**Nokia &#8220;Web&#8221;** and **Bolt** on N95 8GB

<img src="/assets/images/wp-content/misc/css3/nokiaN95_webkit.png" alt="Nokia" /> 
<img src="/assets/images/wp-content/misc/css3/nokiaN95_bolt.png" alt="Bolt" />

note: Android&#8217;s actual screen res is 320&#215;480. The screenshot is not an actual size. (Obviously this is a photograph!). Also the screenshot for iPhone is from emulator but I tested on an actual device as well.

## Summary
        
<table summary="CSS3 Support Chart on various WebKit browsers" class="chart">
  <tr>
    <th>
      Properties
    </th>
    
    <th>
      WebKit Ntly
    </th>
    
    <th>
      iPhone
    </th>
    
    <th>
      Chrome
    </th>
    
    <th>
      Android
    </th>
    
    <th>
      Nokia
    </th>
    
    <th>
      Bolt
    </th>
  </tr>
  
  <tr>
    <td>
      opacity
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="n">
      N
    </td>
  </tr>
  
  <tr>
    <td>
      text-shodow
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="p">
      Y☆
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="n">
      N
    </td>
  </tr>
  
  <tr>
    <td>
      text-overflow (ellipsis)
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="n">
      N★
    </td>
  </tr>
  
  <tr>
    <td>
      border-radius
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="n">
      N
    </td>
  </tr>
  
  <tr>
    <td>
      -webkit-box-shodow
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="n">
      N★
    </td>
  </tr>
  
  <tr>
    <td>
      -webkit-text-stroke
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="n">
      N
    </td>
  </tr>
  
  <tr>
    <td>
      -webkit-text-fill
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="y">
      Y
    </td>
  </tr>
  
  <tr>
    <td>
      -webkit-border-image
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="y">
      Y
    </td>
    
    <td class="n">
      N
    </td>
    
    <td class="y">
      Y
    </td>
  </tr>
</table>
        
☆ Basic feature is spported, but not multiple shodows.

★ Not degraded gracefully. Contents become unreadable so should be avoided.

        
## Additional Notes

Besides the CSS3 test, it is noticeable that Bolt does not honer css font size, weight and header with H tag. This is happening to another J2ME browser, Opera Mini 4 (not tested here since Opera Mini is not WebKit-based). Additionally, like Opera Mini, Bolt uses proxy for rendering and compression. Data is passed through proxy before sending to device.