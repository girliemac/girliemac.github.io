---
title: Creating A Custom HTML5 Form Validation
author: Tomomi Imura
layout: post

categories:
  - CSS
  - Firefox
  - HTML5
  - IE
  - Japanese
  - Mobile
  - Nokia
  - Opera
  - UI/UX
  - WebKit
---

*Note: The article was originally written for [Nokia Code Blog](http://www.developer.nokia.com/Blogs/Code/2012/11/21/creating-a-custom-html5-form-validation/), with helps from Fred Patton (editor) and Andrea Trasatti (proofreading).*

---

In his blog post on [HTML5 forms and IE10 Mobile](http://www.developer.nokia.com/Blogs/Code/2012/11/09/html5-forms-and-ie10-mobile/), Andrea explained HTML5 forms and what is new in Internet Exporer 10 Mobile, so you should now have some understanding of HTML5 form validation. To summarize, HTML5 eases the pain of writing extra logic to validate users’ form inputs, letting you create usable forms with a little or no scripting.

In this tutorial, I will show you a practical example of creating a custom validated form  with CSS3, web fonts, and a bit of JavaScript (or not).

First of all, creating a form field with a simple empty field validation is extremely easy. All you need to do is including required attribute in `<input>`.

```html 
<form> 
  <input type="text" required> 
  <input type="submit" value="Submit"> 
</form> 
```

[Try this simplest form validation demo](http://jsfiddle.net/girlie_mac/X6Uuc/). When you attempt to submit the form with the required field empty, the supported browsers display an error indication (with message, or just a visual indication).

These are the screenshots of default error UI from IE10 (desktop) and IE10 Mobile:  

<img style="vertical-align: top" src="/assets/images/articles/2012/12/screenshot-basic-ie10.png" alt="Basic form validation (IE10)" width="255" height="125" /> <img style="vertical-align: top;margin: 9px 0 0 20px" src="/assets/images/articles/2012/12/screenshot-basic-ie10m.png" alt="Basic form validation (IE10 Mobile)" width="250" height="68" />  

In IE10 Mobile, you do not get the "speech bubble" error message, but the field is focused with red borders while the visual keyboard is popped up, so you know the field needs  attention.

The error message text and its UI vary depending on browsers and language settings. The screenshot below is Chrome running on the MacOS with Japanese as the primary language:
  
<img src="/assets/images/articles/2012/12/screenshot-basic-chrome-jp.png" alt="Basic form validation (Chrome JP)" width="301" height="96" />

OK, this looks good enough, but let’s make it more interesting by customizing it using 1) pattern matching, 2) CSS3 visual effects, and 3) custom error messages.

## Pattern Matching

The `pattern` attribute specifies a regular expression against the control’s value. Here’s a simple regular expression to detect text that is 6 to 12 alphanumeric characters long.


```html 
<form> 
  <input id="username" type="text" pattern="[a-zA-Z0-9_-]{6,12}" autofocus required> 
  <input id="submit" type="submit" value="create"> 
</form> 
```


[Try this demo with the pattern attribute](http://jsfiddle.net/girlie_mac/qe62z/) by submitting an invalid query. For example, type “123″ and hit “Create” button and see what happens.

## CSS3 User Interface Selectors

There are a number of *user interface state pseudo-classes* in CSS. In additional to `:hover`, `:active`, etc., there are more pseudo-classes defined, such as `:valid`, `invalid`, `in-range`, `out-of-range`, `required`, optional, `read-only` and `read-write`.

Let’s color the field input depending on the state. The text will appear red when the entry is invalid, and green when it is valid.

```css 
:valid {
    color: green;
} 
:invalid {
    color: red;
} 
```

[Try this demo](http://jsfiddle.net/girlie_mac/Db7kg/) to see how the CSS takes effect.

## More Visual Effects with Web Font Icon

Now, we are going to display an extra visual indication with a green checkmark icon. Instead of using an image, let’s experiment with CSS3 web font capabilities.
 
<img src="/assets/images/articles/2012/12/screenshot-valid-fonticon.png" alt="using webfont icon" width="269" height="73" />

Before proceeding, if you are not familiar with CSS3 web fonts, please read the articles linked at the end of this blog.

There are many free web fonts out there, as well as some icon fonts you can use for free. In this demo, I used the Iconic font from [IcoMoon](http://icomoon.io/). The great thing about using IcoMoon is that the [IcoMoon App](http://icomoon.io/app/) lets you can choose only the icons you need to use, and package them into a lightweight file.

Once you get the web fonts, upload all the font formats in a one place somewhere on your server with your HTML files, and include the @font-face rule in your CSS file.


```css
@font-face {
    font-family: 'iconic';
    src: url('webfonts/iconic.eot');
    src: url('webfonts/iconic.eot?#iefix') format('embedded-opentype'),
         url('webfonts/iconic.svg#iconic') format('svg'),
         url('webfonts/iconic.woff') format('woff'),
         url('webfonts/iconic.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
}
```

Now, using a CSS trick, add the icon when the entry is in the `:valid` state, with using the `::before` (or `::after`) pseudo-element to insert some content before (or after) the content of an element.

To display the icon after the input field, I am tempted to just use pseudo-class and pseudo-element all together like, `input:valid::after`, However, it is not possible to add contents to the input with the CSS, since input has no document tree content. Therefore, I needed to use an extra element after the input like this:

```html
<input id="username" type="text" pattern="[a-zA-Z0-9_-]{6,12}" autofocus required>
<span class="icon-validation" data-icon="&#xe000"></span> 
```

In the `span`, I am using a `data-` attribute to specify which character to insert. In this case, I am using `data-icon` attribute to hold the special font character that I used IcoMoon to map.


```css
:valid + .icon-validation::before {
    content: attr(data-icon);
    color: green;
}
```

The custom data attributes (`data-*`) in HTML5 is used to store a small private data and retained minimal state on DOM.
You can insert the character directly into the content property of the `::before` pseudo-element in the CSS instead, however, I recommend using the data binding technique with the `data-*` to make your code more semantic.

## Customizing the Error Text

There’s the easy way to customize the message text, and then there’s the easier way.

The easier way is adding inline text with title attribute. The text will be appended after the default error message. The screenshot below is from Opera 12:
  
<img class="alignnone size-full wp-image-329" src="/assets/images/articles/2012/12/screenshot-custom-opera12.png" alt="" width="500" height="150" />

```html
<input id="username" type="text" pattern="[a-zA-Z0-9_-]{6,12}" autofocus required 
       title="must be alphanumeric in 6-12 chars"> 
```

[Try this demo](http://jsfiddle.net/girlie_mac/vuP4n/) to see how this takes in effect.

If you would like to fully customize the error message, you need a little DOM scripting help.
The setCustomValidity method allows you to set a custom text by changeing the validationMessage property of the DOM node that contains the message.

When the input is checked by checkValidity method on a form element node, and found to be invalid, the invalid event is fired for the node. So you can add the event listener to check if the input is either empty or the value is mismatched.

```javascript
input.addEventListener('invalid', function(e) {
    if(input.validity.valueMissing){
        e.target.setCustomValidity("PLZ CREATE A USERNAME, YO!"); 
    } else if(!input.validity.valid) {
        e.target.setCustomValidity("U R DOIN IT WRONG!"); 
    } 
}, false);
```

This is how it looks in Firefox 16.
 
<img src="/assets/images/articles/2012/12/screenshot-custom-ff16.png" alt="" width="250" height="121" />

The `validity` property returns a `ValidityState` object, which contains properties that describe the state (boolean) of validation on an element, such as, value, `valueMissing`, `typeMismatch`, etc. (If you would like to learn more about `ValidityStat`e object, I list some links at the end of this article).

[Try this demo](http://jsfiddle.net/girlie_mac/te3Qd/) to see how it takes effect. I also encourage you to fork the code to play with other `ValidityState` object states.

You can use both the JavaScript and `title` attribute together. Try it by yourself.

## Put Them All Together

I have put together [a full demo](https://dl.dropbox.com/u/1330446/validation.html) with extra styles to mimic the Windows Phone 8 UI, so try it on mobile too!

[<img src="/assets/images/articles/2012/12/form-val-demo-qr.png" alt="Demo URL QR" width="128" height="127" align="right" />][2]  
**http://goo.gl/xKj0X**

These is a little gotcha in IE10 mobile with the icon next to the field—it does not display until the field it unfocused, while on other browsers I have tested, it shows up immediately once the query becomes valid (in this case, when the numbers of the character hits 6).

These are actual screenshots from IE Mobile:

<img src="/assets/images/articles/2012/12/screenshot-ie10m.png" alt="screenshot of IE10 mobile" width="600" height="410" />


## Learn More


*   WebPlatform.org: <a href="http://docs.webplatform.org/wiki/guides/html5_form_features" target="_blank">HTML5 form features</a>
*   Dive Into HTML5: <a href="http://diveintohtml5.info/forms.html" target="_blank">A Form of Madness</a>
*   W3C: <a href="http://www.w3.org/TR/css3-fonts/" target="_blank">CSS Fonts Module Level 3</a>
*   Six Revisions: <a href="http://sixrevisions.com/css/font-face-guide/" target="_blank">The Essential Guide to @font-face</a>
*   WebPlatform.org: <a href="http://docs.webplatform.org/wiki/css/selectors/pseudo-elements" target="_blank">Pseudo-elements</a>
*   MSDN: <a href="http://msdn.microsoft.com/en-us/library/windows/apps/hh466212.aspx" target="_blank">ValidityState object</a>

 [1]: http://jsfiddle.net/girlie_mac/vuP4n/
 [2]: https://dl.dropbox.com/u/1330446/validation.html