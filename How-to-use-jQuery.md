# 📖How to use JQuery

jQuery can be included and used in a web project in several different ways. This guide covers the common approaches, their differences, and the basic setup required to work with jQuery.

## 1. Using jQuery from a CDN

- **A CDN (Content Delivery Network) allows you to load jquery from a server instead of downloading and storing file inside your project.**

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
```

- Once jQuery is loaded, you can use it in your own JavaScript:

```html
<script src="script.js"></script>
```

- The important thing is that **jQuery must be loaded before any JavaScript that depends on jQuery.**

### Popular jQuery CDN Providers

There is no requirement to use one specific CDN. You can use any reliable CDN that provides the required jQuery version.

Some commonly used options are:

Google CDN :

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
```

Microsoft CDN :

```html
<script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.7.1.min.js"></script>
```

CDNJS :

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
```

jsDelivr :

```html
<script src="https://cdn.jsdelivr.net/npm/jquery@3.7.1/dist/jquery.min.js"></script>
```

#### Are all CDNs different?

The CDN providers are different, but if they are serving the same jQuery version and build, the jQuery library itself is essentially the same.

The main differences are in:

- CDN infrastructure
- Server locations
- Network routing
- Availability
- Caching
- Performance
- Provider reliability

> **You normally choose one CDN, not all of them together.**

## 2. Using a Local jQuery File

Instead of using a CDN, you can download jQuery and keep the file inside your project.

jQuery can be downloaded from the official jQuery website:

[Download jQuery](https://jquery.com/download/)

For example, your project could look like:

```text
project/
│
├── index.html
│
├── js/
│   ├── jquery-3.7.1.min.js
│   └── script.js
│
└── css/
    └── style.css
```

Then include jQuery in your HTML:

```html
<script src="js/jquery-3.7.1.min.js"></script>
<script src="js/script.js"></script>
```

**Advantages :**

- No CDN dependency at runtime.
- You control the exact jQuery file used.
- Useful for offline development.
- The library becomes part of your project.

**Disadvantages :**

- You have to manage and update the jQuery file yourself.
- The browser cannot use a CDN-hosted copy.
- Your project size increases slightly.

## 3. Using jQuery with npm

jQuery can also be installed as an npm package.

First, initialize an npm project if you do not already have one:

```bash
npm init -y
```

Then install jQuery:

```bash
npm install jquery
```

jQuery will be added as a project dependency.

You will see something similar to:

```text
project/
│
├── node_modules/
│   └── jquery/
│
├── package.json
├── package-lock.json
└── ...
```

### Using jQuery in JavaScript

In a project that uses a bundler such as Vite or Webpack:

```jsx
import $ from "jquery"

$("#heading").text("Hello jQuery!")
```

> **The bundler handles the dependency and prepares the JavaScript for the browser.**

**Advantages :**

- Dependency is managed through package.json.
- Easy to specify and update the jQuery version.
- Works well with modern JavaScript build tools.
- jQuery can be bundled with the application.

**Disadvantages :**

- Requires Node.js/npm.
- Usually requires a build tool or bundler for browser-based projects.
- More setup than simply adding a CDN <script>.

## 4. Where to Place the Script

**jQuery can be included in both the**

1. head

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>jQuery Practice</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <script src="js/script.js"></script>
  </head>
  <body>
    <h1 id="heading">Hello jQuery</h1>
  </body>
</html>
```

2.body

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>jQuery Practice</title>
  </head>
  <body>
    <h1 id="heading">Hello jQuery</h1>

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
    <script src="js/script.js"></script>
  </body>
</html>
```

Both approaches are valid.
The important rule is:

> jQuery must be loaded before JavaScript code that uses jQuery.

- ## jQuery + `script.js` in the `<head>`

```html
<head>
  <script src="jquery.min.js"></script>
  <script src="script.js"></script>
</head>
```

### How does it work?

The browser parses the HTML from top to bottom. When it encounters a normal `<script>` in the `<head>`, it pauses HTML parsing, downloads and executes the script, and then continues parsing the HTML.

The execution flow is:

```text
HTML parsing
     ↓
Download & execute jQuery
     ↓
Download & execute script.js
     ↓
Continue parsing the body
```

### ✅ Pros

- Scripts are loaded and executed early.
- jQuery is available before `script.js` runs.
- Simple and easy to understand.
- Useful when JavaScript needs to be available before the page content is parsed.
- This approach is commonly shown in basic jQuery tutorials.

### ❌ Cons

- Normal scripts in the `<head>` can **block HTML parsing**.
- The browser may have to download and execute the scripts before continuing to parse the page.
- If the script takes longer to download, the initial rendering of the page can be delayed.
- DOM elements inside the `<body>` may not exist yet when `script.js` executes.

For example, this code may not find the element if it runs before the element is parsed:

```javascript
$("#heading").hide()
```

To wait until the DOM is ready, you can use:

```javascript
$(document).ready(function () {
  $("#heading").hide()
})
```

---

- ## jQuery + `script.js` at the End of `<body>`

```html
<body>
  <h1 id="heading">Hello</h1>
  <button id="btn">Click</button>

  <script src="jquery.min.js"></script>
  <script src="script.js"></script>
</body>
```

### How does it work?

The browser first parses the HTML content of the page. Once it reaches the scripts at the end of the `<body>`, it downloads and executes them.

The execution flow is:

```text
Parse HTML
     ↓
Parse body elements
     ↓
Download & execute jQuery
     ↓
Download & execute script.js
```

At the time `script.js` runs, the elements that appeared before the scripts have already been parsed.

For example:

```html
<h1 id="heading">Hello</h1>

<script src="jquery.min.js"></script>
<script src="script.js"></script>
```

The `#heading` element already exists in the DOM when `script.js` executes.

### ✅ Pros

- Most of the HTML is parsed before the JavaScript executes.
- Initial page rendering is less likely to be blocked by these scripts.
- DOM elements above the scripts are already available.
- Simple and straightforward for small websites and practice projects.
- Often used as a traditional approach for loading JavaScript.

### ❌ Cons

- jQuery and your JavaScript are loaded later in the page lifecycle.
- JavaScript functionality is not available until the browser reaches the scripts.
- If some functionality needs to run before the body is parsed, this approach may not be suitable.
- Modern applications may prefer using `defer` or JavaScript modules instead.

---

- ## `<head>` + `defer` ⭐

A modern approach is to place the scripts in the `<head>` and use the `defer` attribute.

```html
<head>
  <script src="jquery.min.js" defer></script>
  <script src="script.js" defer></script>
</head>
```

### How does `defer` work?

The `defer` attribute tells the browser to download the scripts without blocking HTML parsing.

The scripts are executed **after the HTML has been completely parsed**.

When multiple deferred scripts are present, they execute in the order in which they appear in the HTML.

The execution flow is approximately:

```text
HTML parsing continues
        ↓
jQuery downloads
        ↓
script.js downloads
        ↓
HTML parsing completes
        ↓
jQuery executes
        ↓
script.js executes
```

Therefore:

```html
<script src="jquery.min.js" defer></script>
<script src="script.js" defer></script>
```

ensures that jQuery executes before `script.js`.

### ✅ Pros

- HTML parsing is not blocked while the scripts are downloading.
- Scripts can remain organized inside the `<head>`.
- The DOM has been parsed before the scripts execute.
- The execution order of deferred scripts is preserved.
- Generally provides a better loading pattern than normal blocking scripts in the `<head>`.

### ❌ Cons

- `defer` introduces an additional concept that beginners need to understand.
- Scripts do not execute immediately when they are encountered.
- It is important to understand script dependencies and execution order when using multiple scripts.
- The approach may look different from the basic examples used in beginner tutorials.

## 📌 Important Rule

Regardless of where you place the scripts, **jQuery must be loaded before any JavaScript that depends on it**.

### Correct

```html
<script src="jquery.min.js"></script>
<script src="script.js"></script>
```

### Incorrect

```html
<script src="script.js"></script>
<script src="jquery.min.js"></script>
```

If `script.js` contains:

```javascript
$("#heading").hide()
```

jQuery must already be loaded; otherwise `$` will not be available.

### With `defer`

```html
<script src="jquery.min.js" defer></script>
<script src="script.js" defer></script>
```

The order is still:

```text
jQuery
   ↓
script.js
```

---

## 💡 Which Approach Should You Use?

For **learning and following basic jQuery tutorials**, both the `<head>` and end-of-`<body>` approaches are valid.

For modern projects, placing scripts in the `<head>` with `defer` is often a clean approach:

```html
<head>
  <script src="jquery.min.js" defer></script>
  <script src="script.js" defer></script>
</head>
```

The most important thing is not simply where the scripts are placed, but that:

> **jQuery must be available before your jQuery-dependent code executes.**
