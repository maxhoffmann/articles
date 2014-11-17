---
title: Autoresizing Textareas
date: 2014-02-03
---
# Autoresizing Textareas

For one of my side projects I’ve wanted to use an autoresizing textarea. Besides some jQuery plugins and some pure JavaScript that didn’t work properly I couldn’t find anything useful, so I tried to implement my own solution.

```javascript
var resizingTextareas = [].slice.call(document.querySelectorAll('textarea[autoresize]'));

resizingTextareas.forEach(function(textarea) {
  textarea.addEventListener('input', autoresize, false);
});

function autoresize() {
  this.style.height = 'auto';
  this.style.height = this.scrollHeight+'px';
  this.scrollTop = this.scrollHeight;
}
```

At first the code finds all textareas with an `autoresize` attribute. Then it adds a listener for the input event, which calls the autoresize function. The autorize function sets the textarea’s height to `auto` and immediately changes its height again to its `scrollHeight`. This has to be done otherwise the `scrollHeight` isn’t correcly calculated. The last line ensures that the texarea is scrolled to the bottom whenever a new line is added.

```css
textarea[autoresize] {
  display: block;
  overflow: hidden;
  resize: none;
}
```

Setting the display to `block` prevents a small position change in Chrome, Safari and Opera when the autoresize function is called for the first time. `overflow: hidden` prevents the scrollbars from showing up and `resize: none` removes the small handle at the bottom right corner of the textarea.

You may now use autoresizing textareas like so:

```markup
<textarea autoresize>Type here and I’ll resize.</textarea>
```

You can play around with the code on [JSBin](http://jsbin.com/okUyAgAP/1/edit).
