mqGenie
=======

## Your media queries are wrong!

### mqGenie adjusts CSS media queries in browsers that include the scrollbar's width in the viewport width so they fire at the intended size

WebKit browsers (and Chrome/Blink prior to 29.0.1547.57) are the only browsers that don't include the scrollbar in the viewport. While this is technically incorrect (http://www.w3.org/TR/css3-mediaqueries/#width), it makes sense since scrollbar widths vary across platforms and in the case of "mobile" don't exist.

However, it means that the media queries every Windows developer - and Mac developers who enable scrollbars - write actually fire at a different size when viewed on a mobile device or another OS.

**[View this demo to see mqGenie in action](http://stowball.github.io/mqGenie/)**

#### How does mqGenie work?

* If the browser is "modern" and not one of the above WebKit-based ones, on 'domready' (`DOMContentLoaded`), mqGenie forces a vertical scrollbar on the `<html>` element.
* It then compares `window.innerWidth` to `document.documentElement.clientWidth`. If they're different, this value equals the width of the browser's scrollbar.
* Then it loops through your stylesheets' media queries and increases all of the `min-width` and `max-width` ones by the width of the scrollbar so that they fire at the correct size. It also converts em-based ones, using the HTML's computed `font-size`.

It returns a JavaScript object called `mqGenie`, which contains the following properties: 

* `adjusted` (boolean - whether your media queries were adusted)
* `fontSize` (the computed HTML font-size)
* `width` (the width adjusted by)

A second function, `mqAdjust` is made available, which allows you to re-calculate media queries that are written in JavaScript. Simply pass `mqAdjust` the media query string and it will return one that's adjusted appropriately.

#### Do we need it?

Consider mqGenie as **progressive enhancement**.

Ideally, your responsive projects will be built in a flexible way, such that a 15-20px difference in media queries shouldn't matter too much.

However, there are definitely times where things can go awry. Fixed-width ads and other modules may rely on more precise measurements, and - while I don't condone targeting device widths specifically - writing a 768px media query and not having it triggered on an a portrait iPad, for example, is a little disconcerting.

---

####Usage:

1. Include the tiny (~1.1KB minified and gzipped) mq.genie.js in the `<head>` of your document

2. If you develop in Safari, Chrome/Blink prior to 29.0.1547.57 or Firefox's scrollbar-less RWD View, write your media queries as you always have. mqGenie will adjust them for every other browser as required.

3. If you use another browser (or have scrollbars enabled on Mac), subtract `mqGenie.width` from the browser's reported viewport width. You can use my [Viewport Genie bookmarklet](https://github.com/stowball/Viewport-Genie) to tell you the "actual" viewport size.

4. If you have media queries triggering events in JavaScript, such as with [enquire.js](http://wicky.nillia.ms/enquire.js/), use `mqAdjust(mq-string)` as opposed to `mq-string`

---

Copyright (c) 2013 Matt Stow    
Licensed under the MIT license (see LICENSE for details)    
Minified version created with UglifyJS (http://jscompress.com/)