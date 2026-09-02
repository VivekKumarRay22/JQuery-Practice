# jQuery Events

## What are Events?

**An event is an action or occurrence that a web page can respond to.
An event represents the precise moment when something happens.**

**Examples:**

- Clicking an element
- Moving the mouse over an element
- Pressing a keyboard key
- Submitting a form
- Focusing or leaving an input field

### Event Flow :

```text
User / Browser Action
      ↓
    Event
      ↓
Event Handler
      ↓
  jQuery Code
      ↓
    Action
```

## jQuery Syntax For Event Methods

- Most DOM events have corresponding jQuery event methods.

```js
$("selector").event(function () {
  // action goes here!!
})
```

## Common jQuery Events

- ### `$(document).ready()` :

  The `$(document).ready()` method executes a function when the DOM is ready to be manipulated.

- ### `click()` :

Runs a function when an element is clicked.

```js
$("button").click(function () {
  $("p").hide()
})
```

- ### `dblclick()` :

Runs a function when an element is double-clicked.

```js
$("button").dblclick(function () {
  $(this).hide()
})
```

- ### `mouseenter()` :
  Runs when the mouse pointer enters an element.

```js
$("#box").mouseenter(function () {
  alert("Mouse entered the box!")
})
```

- ### `mouseleave()` :
  Runs when the mouse pointer leaves an element.

```js
$("#box").mouseleave(function () {
  alert("Mouse left the box!")
})
```

- ### `mousedown()` :
  Runs when the mouse button is pressed down over the HTML element.

```js
$("#box").mousedown(function () {
  alert("Mouse button pressed!")
})
```

- ### `mouseup()` :
  Runs when the mouse button is released over the HTML element.

```js
$("#box").mouseup(function () {
  alert("Mouse button released!")
})
```

- ### `hover()` :

  The `hover()` method takes two functions and is a combination of the mouseenter() and mouseleave() methods.

  `hover()` combines:

```text
  mouseenter()
        +
  mouseleave()
        ↓
     hover()
```

> **The first function is executed when the mouse enters the HTML element, and the second function is executed when the mouse leaves the HTML element:**

```js
$("#box").hover(
  function () {
    // mouse enters
  },
  function () {
    // mouse leaves
  },
)
```

- ### `focus()` :
  The `focus()` method attaches an event handler function to an HTML form field.
  The function is executed when the form field gets focus:

```js
$("input").focus(function () {
  $(this).css("background-color", "yellow")
})
```

- ### `blur()` :
  The `blur()` method attaches an event handler function to an HTML form field.
  The function is executed when the form field loses focus:

```js
$("input").blur(function () {
  $(this).css("background-color", "green")
})
```

> `focus()` and `blur()` : These are commonly used with form inputs.

```text
Click input
    ↓
 focus()
    ↓
Input loses focus
    ↓
 blur()
```

- ### `on()` :
  The `on()` method attaches one or more event handlers for the selected elements.

**Single Event**

```js
$("p").on("click", function () {
  $(this).hide()
})
```

**Multiple Events**

```js
$("#box").on({
  mouseenter: function () {
    $(this).css("background-color", "grey")
  },

  click: function () {
    $(this).css("background-color", "green")
  }
})
```
