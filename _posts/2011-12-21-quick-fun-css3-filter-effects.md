---
title: 'Quick Fun: CSS3 Filter Effects'
author: Tomomi Imura
layout: post
permalink: /blog/2011/12/21/quick-fun-css3-filter-effects/
topsy_short_url:
  - http://is.gd/ww3fYB
  - http://is.gd/ww3fYB
categories:
  - CSS
  - Sandbox
  - Uncategorized
  - WebKit
---
I quickly played with the brand-new <a href="https://dvcs.w3.org/hg/FXTF/raw-file/tip/filters/index.html" target="_blank">CSS Filter Effects</a> on the latest <a href="http://nightly.webkit.org" target="_blank">WebKit Nightly</a>! (Edited: Now also supported on <a href="http://tools.google.com/dlpage/chromesxs" target="_blank">Chrome Canary</a> 18.0.976.0 +)

Click the images to view in the full size.

[<img src="/assets/images/wp-content/uploads/2011/12/default-300x235.png" alt="no filter" title="no filter" width="300" height="235" align="left" size-medium wp-image-412" />][1]  
This is a default google.com screen.  
No filter added.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/blur-2px-300x235.png" alt="filter:blur(2px)" title="filter:blur(2px)" width="300" height="235" align="left" size-medium wp-image-413" />][2]  
**blur(radius)** to create Gaussian blur

```css
-webkit-filter: blur(2px);
```

The default is 0, no blur.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/brightness-30-300x235.png" alt="filter:brightness(30%)" title="filter:brightness(30%)" width="300" height="235" align="left" size-medium wp-image-416" />][3]  
**brightness(amount)**

```css
-webkit-filter: brightness(30%);
```

<del>The default is 100%. Values of amount over 100% are allowed.</del>  
**Updated**: I am not sure when it has modified, but it seems that not the accepted value is the range between -100% (dark) and 100% (light), and the default is 0.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/contrast-30-300x235.png" alt="filter:contrast(30%)" title="filter:contrast(30%)" width="300" height="235" align="left" size-medium wp-image-418" />][4]  
**contrast(amount)**

```css
-webkit-filter: contrast(30%);
```

The default is 100%. Values of amount over 100% are allowed.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/grayscale-100-300x235.png" alt="filter:grayscale(100%)" title="filter:grayscale(100%)" width="300" height="235" align="left" size-medium wp-image-419" />][5]  
**grayscale(amount)**

```css
-webkit-filter: grayscale();
```

The default is 100%.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/sepia-100-300x235.png" alt="filter:sepia(100%)" title="filter:sepia(100%)" width="300" height="235" align="left" size-medium wp-image-420" />][6]  
**sepia(amount)**

```css
-webkit-filter: sepia();
```

The default is 100%.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/invert-100-300x235.png" alt="filter:invert(100%)" title="filter:invert(100%)" width="300" height="235" align="left" size-medium wp-image-421" />][7]  
**invert(amount)**

```css
-webkit-filter: invert();
```

The default is 100%.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/opacity-30-300x235.png" alt="filter:opacity(30%)" title="filter:opacity(30%)" width="300" height="235" align="left" size-medium wp-image-422" />][8]  
**opacity(amount)**

```css
-webkit-filter: opacity(30%);
```

The default is 100%, no transparency.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/saturate-50-300x235.png" alt="filter:saturate(50%)" title="filter:saturate(50%)" width="300" height="235" align="left" size-medium wp-image-423" />][9]  
**Saturate(amount)**

```css
-webkit-filter: saturate(50%);
```

The default is 100%.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/saturate-300-300x235.png" alt="filter:saturate(300%)" title="filter:saturate(300%)" width="300" height="235" align="left" size-medium wp-image-436" />][10]  
**Saturate(amount)** &#8211; the amount over 100% is also allowed.

```css
-webkit-filter: saturate(300%);
```

<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/hue-rorate-90deg-300x235.png" alt="filter:hue-rotate(90deg)" title="filter:hue-rotate(90deg)" width="300" height="235" align="left" size-medium wp-image-424" />][11]  
**hue-rotate(angle)**

```css
-webkit-filter: hue-rotate(90deg);
```

The default is 0deg.  
<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/hue-rorate-300deg-300x235.png" alt="filter:hue-rotate(300deg)" title="filter:hue-rotate(300deg)" width="300" height="235" align="left" size-medium wp-image-425" />][12]  
**hue-rotate(angle)**

```css
-webkit-filter: hue-rotate(300deg);
```

<br clear="all" />

[<img src="/assets/images/wp-content/uploads/2011/12/drop-shadown-on-toolbar-300x235.png" alt="filter:drop-shadow(...)" title="filter:drop-shadow(...)" width="300" height="235" align="left" size-medium wp-image-441" />][13]  
**drop-shadow(<shadow>)**

```css
/* Adding Drop-shadow on the toolbar at the top */

#bg {
  -webkit-filter: drop-shadow(rgba(0,0,0,0.5) 0 5px 5px);
}
```

<br clear="all" />

 [1]: /assets/images/wp-content/uploads/2011/12/default.png
 [2]: /assets/images/wp-content/uploads/2011/12/blur-2px.png
 [3]: /assets/images/wp-content/uploads/2011/12/brightness-30.png
 [4]: /assets/images/wp-content/uploads/2011/12/contrast-30.png
 [5]: /assets/images/wp-content/uploads/2011/12/grayscale-100.png
 [6]: /assets/images/wp-content/uploads/2011/12/sepia-100.png
 [7]: /assets/images/wp-content/uploads/2011/12/invert-100.png
 [8]: /assets/images/wp-content/uploads/2011/12/opacity-30.png
 [9]: /assets/images/wp-content/uploads/2011/12/saturate-50.png
 [10]: /assets/images/wp-content/uploads/2011/12/saturate-300.png
 [11]: /assets/images/wp-content/uploads/2011/12/hue-rorate-90deg.png
 [12]: /assets/images/wp-content/uploads/2011/12/hue-rorate-300deg.png
 [13]: /assets/images/wp-content/uploads/2011/12/drop-shadown-on-toolbar.png