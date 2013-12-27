---
title: HTML5 Form Field Validation with CSS3
author: Tomomi Imura
layout: post
permalink: /blog/2011/11/28/html5-form-field-validation-with-css3/
topsy_short_url:
  - http://is.gd/OOiBZI
  - http://is.gd/OOiBZI
dsq_thread_id:
  - 2067880933
categories:
  - CSS
  - HTML5
  - UI/UX
---
## HTML5 Built-in Form Validation


HTML5 specifications come with a full of goodness that make web developer's lives easier.  
The one of the goodies, the client form validation is the one I like a lot, because, for example, by adding `required` attribute to an `input`, I don&#8217;t need to write any additional JavaScript to warn a user, when the user submits a form without filling out the required fields. The interactive warning UI comes with browsers.

<img src="/assets/images/wp-content/uploads/2011/11/form-validation-required.png" alt="screenshot" title="form-validation-required" width="400" height="120" />

The &#8220;Speech bubble&#8221; UI is built in with HTML5-enabled browsers. (This screenshot is taken on Chrome. Other browsers like Firefox and Opera have their own interface.)

### Pattern Matching

You can also validate against patterns that defined by you. The `pattern` attribute specifies a regular expression against the control&#8217;s value.

```html
<input type="text" pattern="[0-9]{13,16}" title="A credit card number" />
```

A user is required to enter values to match a regular expression pattern, in this case, a 13 to 16 digit number. 

## CSS3 User Interface Selectors

There are numerous *user interface state pseudo-classes*. You&#8217;ve probably already known `:hover`, `:active` etc. According to this <a href="http://www.w3.org/TR/css3-ui/#user-interface" target="_blank">W3C Candidate Doc</a>, there are additional pseudo-classes defined, such as `:valid`, `invalid`, `in-range`, `out-of-range`, `required`, `optional`, `read-only` and `read-write`.

So I played a bit with `:valid` and `:invalid` to check against the regular expression pattern.

<img src="/assets/images/wp-content/uploads/2011/11/form-validation.png" alt="Form validation screenshot" title="form-validation" width="401" height="313" />

The diagram shows: 1) The entry is displayed in red when the entered text is not matched.  
2) The built-in HTML5 message is displayed when the user submits the form while leaving the invalid entry. No additional CSS is used.  
3) The entry is in green when it matches with the defined pattern. Also, a check mark is used as an indicator to tell it is valid.

The simplified code is below. Also you can view the entire code and the working demo on <a href="http://jsfiddle.net/girlie_mac/rdkmY/" target="_blank">jsFiddle</a>.

```html
<input id="cc" type="text" pattern="[0-9]{13,16}" required />
<div class="input-validation"></div>
<input id="payButton" type="submit" value="Pay Now" />
```

```css
input[type="text"]:valid {
    color: green;
}

input[type="text"]:valid ~ .input-validation::before {
    content: "✓";
    color: green;
}

input[type="text"]:invalid {
    color: red;
}
```

I was too lazy to create an image, so I just used the unicode checkmark. Actually, what I wanted to do was that inserting the unicode content after the input with this CSS- `input:valid:after`. However, it is not possible to add contents to the input with the CSS since `input` has no document tree content. Therefore, I used the extra `div` after the input. (So I am using the sibling selector, `~`, to specify the div).

If you would make it prettier, I suggest you should place some icons as a background-image of the input, instead of just dumping some unicode char!

```css
input[type="text"]:valid {
    background: url(thumb-up.png) no-repeat top right;
}
```

---

*Note: Also, I wrote an updated article on HTML5 forms on <a href="http://developer.nokia.com/Blogs/Code/2012/11/21/creating-a-custom-html5-form-validation/" target="_blank">Nokia Code Blog</a> in November 2012. Read it too if you liked this article!*

---

## References

<a href="http://blog.mozilla.com/webdev/2011/03/14/html5-form-validation-on-sumo/" target="_blank">HTML5 Form Validation on SUMO</a> (Mozilla Blog)

<a href="http://www.w3.org/TR/css3-ui/#pseudo-validity" target="_blank">CSS3 Basic User Interface Module</a> by W3C

<a href="http://www.whatwg.org/specs/web-apps/current-work/multipage/common-input-element-attributes.html#the-pattern-attribute" target="_blank">The pattern attribute</a> by WHATWG 

<a href="http://html5pattern.com" target="_blank">HTML5 Patterns</a>