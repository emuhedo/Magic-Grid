[![MIT License](https://img.shields.io/npm/l/magic-grid.svg?style=for-the-badge)](https://www.npmjs.com/package/magic-grid)
[![Version](https://img.shields.io/npm/v/magic-grid.svg?style=for-the-badge)](https://www.npmjs.com/package/magic-grid)

# Magic Grid
## A simple, lightweight Javascript library for dynamic grid layouts.

Creating a dynamic grid layout has never been easier. With Magic Grid, all you have to do is specify a container and listen for changes. A few other configuration options are available for convenience but it's all very simple. Check it out live <b>[on JSFIDDLE](https://jsfiddle.net/eolaojo/4pov0rdf/)</b>. You can read about the implementation details <b>[on CodeBurst](https://codeburst.io/magic-grid-f8e2221e7cef)</b>.

**Note: Every item in the grid must have the same width.**

#### [Sample Usage](https://github.com/e-oj/Magic-Grid/blob/master/test/grid.html)

<img src="http://drive.google.com/uc?export=view&id=172ESPZDwQIf7vLMelun-_4RaWD_-j94-" alt="demo" width="850"></img>

#### [@imlinus](https://github.com/imlinus) has created a Vue.js port of the library. You can check it out [here](https://github.com/imlinus/Vue-Magic-Grid).

### Why not CSS Grid?

This question is addressed in <b>[the article](https://codeburst.io/magic-grid-f8e2221e7cef)</b>:

> Implementing a grid layout can quickly turn into a tricky task. If you have grid items that are always the same height, then you can probably make do with a Flexbox grid or some other CSS grid implementation. However, if you’re dealing with user-generated content, chances are, you don’t have the luxury of equal height components. One longer or shorter component would either stretch the other components in its row, or leave some unpleasant whitespace at the bottom of the row. All of a sudden, our beloved CSS grid has become insufficient.

Check out <b>[CSS Grid AMA's issue #19](https://github.com/rachelandrew/cssgrid-ama/issues/19)</b> for a response from CSS expert <b>[@rachelandrew](https://github.com/rachelandrew)</b>:

> That's not something grid is designed for. Grid is two dimensional so you are always working in both rows and columns at the same time. You can't use grid to do a "masonry" style layout like that. You could place items in that way if you had a lot of rows and managed how many each spanned, but you can't use auto-placement to get that kind of layout.

### Getting Started
#### Step 1

Get Magic Grid via NPM:

```
npm install magic-grid
```

Or CDN
```html
<script src="https://unpkg.com/magic-grid/dist/magic-grid.cjs.js"></script>

<!-- or (minified) -->
<script src="https://unpkg.com/magic-grid/dist/magic-grid.min.js"></script>
```

#### Step 2 (skip if using CDN)

Import Magic Grid:

```javascript
import MagicGrid from "magic-grid"

// or
let MagicGrid = require("magic-grid");
```
<br>

You can also pull Magic Grid directly into your html

```html
<script src="node_modules/magic-grid/dist/magic-grid.cjs.js"></script>

<!-- or (minified) -->
<script src="node_modules/magic-grid/dist/magic-grid.min.js"></script>
```

#### Step 3

You're good to go! If you used a script tag, the library can be referenced via the global variable, MagicGrid.

```javascript
let magicGrid = new MagicGrid(...);

magicGrid.listen();
```

### Usage
#### Static content:
If your container doesn't have any dynamically loaded content i.e., all its child elements are always in the DOM, you should initialize the grid this way:
```javascript
let magicGrid = new MagicGrid({
  container: "#container", // Required. Can be class, id selector or HTMLElement.
  static: true, // Required for static content.
  animate: true, // Optional.
});

magicGrid.listen();
```

#### Dynamic content:
If the container relies on data from an api, or experiences a delay, for whatever reason, before it can render its content in the DOM, you need to let the grid know the number of items to expect:
```javascript
let magicGrid = new MagicGrid({
  container: "#container", // Required. Can be class, id selector or HTMLElement.
  items: 20, // For a grid with 20 items. Required for dynamic content.
  animate: true, // Optional.
});

magicGrid.listen();
```

### API

#### MagicGrid(config)
 > config (required): Configuration object

The MagicGrid constructor. Initializes the grid with a configuration object.
```javascript
let magicGrid = new MagicGrid({
  container: "#container", // Required. Can be class or id of the container or HTMLElement.
  static: false, // Required for static content. Default: false.
  items: 30, // Required for dynamic content. Initial number of items in the container.
  gutter: 30, // Optional. Space between items. Default: 25(px).
  maxColumns: 5, // Maximum number of columns. Default: Infinite.
  useMin: true, // Prioritize shorter columns when placing items in the grid. Default: false.
  animate: true, // Animate item positioning. Default: false.
});
```

---

#### .listen()
Positions the items and listens for changes to the window size. All items are repositioned whenever the window is resized.
```javascript
let magicGrid = new MagicGrid({
  container: "#container", // Required. Can be class, id selector or HTMLElement.
  static: true, // Required for static content.
  animate: true, // Optional.
});

magicGrid.listen();
```

---

#### .positionItems()
This function is useful in cases where you have to manually trigger a repositioning; for instance, if a new element is added to the container.

```javascript
let magicGrid = new MagicGrid({
  container: "#container", // Required. Can be class, id selector or HTMLElement
  items: 30, // Required for dynamic content.
  animate: true, // Optional
});

magicGrid.listen();

// get data from api
// append new element to DOM

// reposition items
magicGrid.positionItems();
```

---
