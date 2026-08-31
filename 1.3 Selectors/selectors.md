# jQuery selectors

**jQuery selectors allow you to select and manipulate HTML element(s).jQuery selectors are based mainly on CSS selectors, along with some jQuery-specific selectors.**

## 1. Element Selector

Selects all elements based on their HTML tag name.

```html
$("p");
```

selects all `p` elements
selects

## 2. ID Selector

- Selects an element using its id.
- An id should be unique within a page, so you should use the #id selector when you want to find a single, unique element.

```html
$("#id-name");
```

`#` is used before the ID.

## 3. Class Selector

- Selects elements using their class.

```html
$(".class-name");
```

`.` is used before the class name.

## 4. Universal Selector

Selects all HTML elements.

```html
$("*");
```

Example:

```html
$("*").hide();
```

This hides all elements on the page.

## 5. $(this)

Selects the current HTML element.

```js
$("button").click(function () {
  $(this).hide()
})
```

Here, only the button that is clicked will be hidden.

## 6. Combining Selectors

Multiple selectors can be combined using a comma.

```js
$("h1, p, .box")
```

```text
This selects:

<h1> elements
      +
<p> elements
      +
elements with class="box"
```

## 7.More Useful Selectors

jQuery also supports many CSS-style and jQuery-specific selectors.

| Selector                   | Description                                              |
| -------------------------- | -------------------------------------------------------- |
| `$("p.intro")`             | `<p>` elements with class `intro`                        |
| `$("p:first")`             | First `<p>` element                                      |
| `$("ul li:first")`         | First `<li>` element of the first `<ul>`                 |
| `$("ul li:first-child")`   | First `<li>` element of every `<ul>`                     |
| `$("[href]")`              | Elements having an `href` attribute                      |
| `$("a[target='_blank']")`  | `<a>` elements whose `target` is `_blank`                |
| `$("a[target!='_blank']")` | `<a>` elements whose `target` is not `_blank`            |
| `$(":button")`             | `<button>` elements and `<input type="button">` elements |
| `$("tr:even")`             | Even `<tr>` elements                                     |
| `$("tr:odd")`              | Odd `<tr>` elements                                      |
