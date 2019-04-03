---
title: Reiwa - JavaScript International Date Format and Japan's New Imperial Era 
author: Tomomi Imura
layout: post
description: The reign of the next emperor in Japan means you need to know about JavaScript international date and time format!
categories:
  - Intl.DateTimeFormat
  - javascript
  - internationalization
  - japan

---

As Emperor Akihito of Japan is set to abdicate soon, the Japanese government announced on April 1st that the reign of the next emperor will be known as the Reiwa (令和) era.

![reiwa](https://cdn.cnn.com/cnnnext/dam/assets/190401111401-yoshihide-suga-reiwa-announcement-exlarge-169.jpg)

You may wonder like, "Wait, Japan hasn't adopted the Gregorian calendar system!?" -- Well, yes Japan did over 100 years ago, however, Japan use both "Western" calendar and the unique Japanese Imperial year, which is based on the legendary foundation of Japan by Emperor Jimmu in 660 BC.

Anyway, what I want to talk about in my blog is not about Japanese history but JavaScript `Intl.DateTimeFormat` object that enable language and locale specific date and time formatting.

[The ECMAScript Internationalization API](https://tc39.github.io/ecma402/) was originally introduced in 2010, and currently in the 6th Edition, to help localize the output of dates, numbers, and currencies in Javascript. And this has been well supported by major browsers now. (See [Can I use](https://caniuse.com/#search=Intl))

One of the property of the `Intl` object is [`DateTimeFormat`](https://tc39.github.io/ecma402/#datetimeformat-objects), which enable language and locale specific date and time formatting. 

So yes, with the `Intl.DateTimeFormat` object, you can automatically print out the Japan local date and time with Japanese imperial era!

## Using DateTimeFormat

Without specifying a locale / language, `DateTimeFormat` uses the default locale and the default time zone, so when I am on my machine in the US:

```js
new Intl.DateTimeFormat().format(Date.now())
```
returns today's date in en-US as: 

```
"4/2/2019"
```

### Specifying Locales

You can get a localized date and time by using a locale identifier (language code and a country/region code) as the `locales` argument,  for example:

```js
new Intl.DateTimeFormat('ru-RU').format(Date.now())

// "02.04.2019"
```
and Japan is:
```js
new Intl.DateTimeFormat('ja-JP').format(Date.now())

// "2019/4/2"
```

Okay, but you still see the Gregorian calendar year here. So how can you make it fully localized with Imperial year?

Well, the locale identifier, `ja-JP`, is not enough and you need to add an extention `-u-ca-japanese`. I don't know exactly what it means but all I can say is `ja-JP-u-ca-japanese` is an awkwardly complicated local code.

>
Edited: Thank you, [ジャンクリストフ](https://twitter.com/brandelune) for letting me know that `-u` in the identifier indicates an extension, `-ca` says defines a type of calendar, in this case, `-japanese` calendar.
For more info on locale data, see: [Unicode Technical Standard #35](http://www.unicode.org/reports/tr35/#Locale_Extension_Key_and_Type_Data)


```js
new Intl.DateTimeFormat('ja-JP-u-ca-japanese').format(Date.now())

// "31/4/2"
```
Now, we know it is the year 31. But what year is it? How can we know the Imperial name!?

To get the whole deal, use the `options` argument, in this case use `era`:

```js
new Intl.DateTimeFormat('ja-JP-u-ca-japanese', {era:'long'}).format(Date.now())

// ta-da! "平成31年4月2日"
```

Oooh yeah, now you get "平成31年4月2日"!

Let's try one more thing with Thai locale:

```js
new Intl.DateTimeFormat('th-TH-u-nu-thai', {era:'long'}).format(Date.now())

// "๒ ๔ พุทธศักราช ๒๕๖๒"
```
Woooh, I have no idea how to read this, but it is the year 2562 in Buddhist calendar!


Well, you can find details on the options and learn more about this topic on  [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat)

Also, I quickly wrote up this silly little web app called **Is it Reiwa (令和) yet?** on [https://reiwa-yet.glitch.me/](https://reiwa-yet.glitch.me/). This should say **No** until May 1, 2019, when Crown Prince Naruhito becomes a new emperor, the imperial year should be changed to 令和元年, *if the new era is implemented in your browser!!!* So let's update your browser and see!

---

By the way, I totally didn't blog on my own website last year, as writing technical tutorials has become a part of my day job, I don't write when I am not paid as often. I hope I can start writing random technical posts again.
