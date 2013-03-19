mqGenie
=======

### Adjusts CSS media queries in browsers that include the scrollbar's width in the viewport width so they fire at the intended size

WebKit browsers are the only browsers that don't include the scrollbar in the viewport. While this is technically incorrect (http://www.w3.org/TR/css3-mediaqueries/#width), it makes sense as mobile devices don't have scrollbars.

If not already applied with CSS, mqGenie forces a vertical scrollbar on `<html>`. If the browser is not WebKit based, mqGenie increases all of the media queries by the width of the scrollbar so that they fire at the correct size - including em based ones.

It returns a JavaScript object called `mqGenie`, which contains the following properties: 

* `adjusted` (boolean)
* `fontSize` (computed HTML font-size)
* `width` (scrollbar width)

A second function, `mqAdjust` is made available, which allows you to re-calculate media queries that are written in JavaScript. Simply pass `mqAdjust` the media query string and it will return one that's adjusted appropriately.

---

***Usage:***

1. Include mq.genie.min.js in the `<head>` of your document

2. If you develop in Chrome or Safari, write your media queries as you always have. If you use another browser, subtract `mqGenie.width` from the browser's reported viewport width.

3. If you have media queries triggering events in JavaScript, such as with enquire.js, use `mqAdjust(string)` as opposed to `string`

---

Minified version created with YUI Compressor (http://www.refresh-sf.com/yui/)