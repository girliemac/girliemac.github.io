---
title: Spread Syntax "Three-dots" Tricks You Can Use Now
author: Tomomi Imura
layout: post
description: Want to consume more syntactic sugar to energize your code? I'll share 6 tricks with the spread syntax that you can use now!
images:
  - assets/images/articles/2020/06/es6-spread.png
categories:
  - ES6
  - javascript
  - dev
  - tips
---

*This articles is created based on my own [tweet](https://twitter.com/girlie_mac/status/1263955788990566400) posted on May 22, 2020*

![ES6 tricks](https://res.cloudinary.com/practicaldev/image/fetch/s--fca3o3sF--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/i/4mqpk334i9k78gaw6q7n.png)

ES6 (ECMAScript 2015, the 6th edition) was finalized 5 years ago, and brought us a significant amount of new syntax and features to help you write complex code better and simpler. 

I am assuming that many of you have consumed more calories from the syntactic sugar by adopting new features like class declarations, `let` / `const`, and arrow function expression, and so on, but how about some of the lesser-known [Spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)? 

Here, I would like to share some good usages of spread operator, a.k.a three-dots that I've found while I was coding (and StackOverflowing, I don't lie about how I code!). 

## What do Three Dots do?

First, there are two "three-dots" sugars introduced in ES6. One is [**Rest parameter**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters), which allows us to use an arbitrary number of arguments, and another is **Spread operator**, which also has the similar syntax with three dots, but it is more like the reversed version- it takes the array itself, not arguments. 

In this article, I am showing tricks that uses spread syntax. Looking at the practical examples may be far easier to understand what it does than by reading the definitions!

---

## Concat 

You say "cat" so I say meow. 

Let's concatenate two arrays. Here we have two arrays that represent cat fur coat colors: 

```js
const arr1 = ['solid', 'bicolor', 'tabby'];
const arr2 = ['calico', 'tortoiseshell'];
```

This is how we traditionally did before ES6 using `concat()`:

```js
var conCats = arr1.concat(arr2);
// ['solid', 'bicolor', 'tabby', 'calico', 'tortoiseshell']
```

Now you can simply write with the ES6 spread syntax like this:
```js
const conCats = [...arr1, ...arr2]; 
// ['solid', 'bicolor', 'tabby', 'calico', 'tortoiseshell']
```

## Convert a string to array 

Have you been asked to reverse a string, or check if a string is a palindrome at job interviews? The questions you got may be more complex, but these are pretty common interview questions for software engineers. 

Anyway, the first step to solve the question is likely to convert the given string to an array.

You have a given string:

```js
const str = 'kitty';
```

With pre-ES6 JavaScript, use `split()` to get each letter in an array:

```js
var newArr = str.split(''); // ['k', 'i', 't', 't', 'y'];
```

Now with the ES6 spread syntax, you can achieve the same as:

```js
const newArr = [...str]; // ['k', 'i', 't', 't', 'y'];
```

## Find Max or Min

Let's say, you have a given set of numbers,

```js
10, 9, 6, 12 
```
To find the largest (or smallest) number from the set of numbers, you can use `Math.max()` (or `Math.min()`) and pass the given numbers as input parameters like this: 

```js
var max = Math.max(10, 9, 6, 12);
```

Now with the ES6 spread syntax, you can pass an array of numbers: 

```js
const nums = [10, 9, 6, 12];
const max = Math.max(...nums); // 12
```

## Copy an Array

You can also create a shallow copy of an array with the spread syntax.

You have an array,

```js
const allCatNames = ['chewie', 'leia', 'yoda', 'chewie', 'luke', 'leia'];
```

And onne way to get a shallow copy of the array with the pre-ES6 is using `slice()`:

```js
var allCatNamesCopy = allCatNames.slice();
```

Now with ES6 spread syntax, you can simply do:

```js
const allCatNamesCopy = [...allCatNames];
```

## Remove Dups from an Array

The array, `allCatNames` above has some duplicated values (`chewie` and `leia` appeared twice in the list). If want to remove the duplicates, you'll write multiple lines of code with pre-ES6 JavaScript- 

You probably would iterate the array. And at each loop, map each value in an object to track if the key in the object is unique, and if yes, the value is pushed to a new array. Then at the end of the loop, you have the new array only with unique values.

You can actually achieve this in one line of code with spread syntax by creating a new array with combination of the spread syntax with the `Set` object:

```js
const catNames = [...new Set(allCatNames)]; 
// ['chewie', 'leia', 'yoda', 'luke'];
```
Ta-da, this saves a lot of code!

## Collecting HTML Elements in an Array

If you are a front-end JavaScript developer, this trick may be useful when you manipulate DOM-

Let's say, when you re trying to grab every element with the class name, `.cat`, you probably use `querySelectorAll()` to get the collection of the DOM nodes.

But `document.querySelectorAll('.cat')` returns a static *NodeList*, which is an array-like, but not exactly an array that you can iterate over it.

So in some occasions, you need to convert a NodeList to Array. Traditionally, you probably have been writing code like this, which doesn't seem so intuitive:

```js
var catElementArray = [].slice.call(document.querySelectorAll('.cat'));
```

Now with the spread syntax, you can rewrite as followings:

```js
const catElementArray = [...document.querySelectorAll('.cat')];
```

This looks more intuitive, doesn't it?

---

Well, if you like the three-dots notation or not, now you see that the spread operator can be quite handy when you work with arrays and objects.

I would be happy if I just convinced you to use the three-dots in your daily code from now on. Surely, there are more clever ways to write code with using the spread operator, so if you know the tricks, please share with me and the rest of the JS community!

### Wants to find out more about ES.Next? 

I will be giving a talk, *ECMeowScript - What’s new in JavaScript Explained with Cats* at [Forward JS](https://forwardjs.com/) (~~San Francisco~~ virtual) in July and [Web Directions](https://webdirections.org/) (~~Sydney~~ virtual) in September, so I hope you can catch my talk! 🐱


Ciao!