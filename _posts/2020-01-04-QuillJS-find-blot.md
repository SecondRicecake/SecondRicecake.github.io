---
title: "Quill JS - how to find blot"
categories:
  - how-to-do-stuff
excerpt_separator: "<!--more-->"
tags:
  - QuillJS
  - Parchment
  - Brainlog
---

## Short Brainlog Post

**Goal**: I want an easy way to reselect a piece of text I already formatted.

**Problem**: So how do I select a blot within the editor?

**Solution**:

1. Add an eventlistener to the editor div.
2. Simply using the offset value from the event target does not work as `quill.setSelection(index, length)` needs index value of the blot.
3. Import Parchment, and use the `find()` function to find the blot.
4. Then use the `offset()` function taking _quill.scroll_ as a parameter. This will return the index of the blot.
5. Use the `setSelection()` function to set the selection.

```javascript
const Parchment = Quill.import("parchment");

document.addEventListener("click", () => {
  if (e.target) {
    let blot = Parchment.find(e.target);
    let index = blot.offset(quill.scroll);
    quill.setSelection(index, e.target.textContent.length);
  }
});
```

_This code was partially taken from [QuillJS Issue](https://github.com/quilljs/quill/issues/1115)_
