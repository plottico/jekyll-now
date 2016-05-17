---
layout: post
title: Convert all IMG to OBJECT tags on the page
comments: true
snippet: false
---

The recommended way of embedding SVG images is using an `<OBJECT>` html tag. But there are cases where this tag is not supported by the site editor.
To help converting all `<IMG>` tags that are pointing to plotti.co plots to `<OBJECT>`s you can just drop this script onto your site:

```javascript
window.addEventListener("load", function load(event) {
window.removeEventListener("load", load, false);
setInterval(function() { var limg = document.getElementsByTagName("IMG");
var r = new RegExp("^(http:|https:|)\/\/plotti.co");
for(var il=0; il<limg.length; il++) { var s = limg[il].getAttribute("src"); if(r.test(s)) {
var p = limg[il].parentNode; var st = limg[il].getAttribute("style");
var cl = limg[il].getAttribute("class"); var o = document.createElement("object");
o.setAttribute("data", s); o.setAttribute("type", "image/svg+xml");
o.setAttribute("class", cl); o.setAttribute("style", st);
p.replaceChild(o,limg[il]);}}}, 1000); },false);
```
it will periodically check for plots that should be converted, and will convert them in-place.

Tags: javascript, IMG, object
