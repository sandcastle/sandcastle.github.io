---
date: 2014-12-14
title: "Turn any webpage into a WYSIWYG editor with HTML5"
tags: [ "html", "web", "code" ]
categories: [ "development" ]
---

There is a little known feature in the HTML5 spec that enables you to turn an entire page or a single element into a [WYSIWYG](http://en.wikipedia.org/wiki/WYSIWYG) editor with a single line of JavaScript and its [supported by every major browser](http://caniuse.com/#feat=contenteditable) out there.

To enable you simply set the `contentEditable` attribute of an element to `true`:

```javascript
// make the entire website editable
document.body.contentEditable = true;

// make an element editable
document.getElementById('myDiv').contentEditable = true;
```

To check if an element is editable you check the `isContentEditable` attribute:

```javascript
if (document.getElementById('myDiv').isContentEditable){
  // yes its editable
}
```

Both `contentEditable` and `isContentEditable` are described in the [HTML5 Editing spec](http://www.w3.org/TR/html5/editing.html#contenteditable).
