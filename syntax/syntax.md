# jQuery syntax

The jQuery syntax is tailor-made for selecting HTML elements and performing some action on the element(s).

- the basic syntax is

```js
$(selector).action()
```

- **Think like this**

```text
$          (selector)          .action()
│              │                   │
│              │                   └── What to do
│              └────────────────────── Which element(s)
└───────────────────────────────────── jQuery

```

Example :

```js
$("p").hide()
```

- **`$` - jQuery Shortcut (to access jQuery)**
- **`p` - selector;"query (or find)" to select elements**
- **`.hide()` - what action to perform on selected element**

## The Document Ready Event

- This is to prevent any jQuery code from running before the document is finished loading (is ready).

- It is good practice to wait for the document to be fully loaded and ready before working with it. This also allows you to have your JavaScript code before the body of your document, in the head section.

```js
$(document).ready(function () {
  // jQuery code
})
```

## Shorter ready() Syntax

**This**

```js
$(function () {
  $("#heading").hide()
})
```

**same as**

```js
$(document).ready(function () {
  $("#heading").hide()
})
```
