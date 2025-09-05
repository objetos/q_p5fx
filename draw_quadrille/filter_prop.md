---
weight: 9
draft: false
title: filter
---

Filters which cells to draw from a given quadrille `q`. It accepts the following types:

* **A value collection (`Array` or `Set`)**
  Draws only the cells whose values are included in the collection.
  [Example](#example-filtering-by-value-collection):
  `drawQuadrille(q, { filter: [red, blue] })`

* **A predicate function over the *cell* (`(cell) => boolean`)**
  The function receives `{ row, col, value }` and must return `true` to draw that cell.
  [Example](#example-filtering-by-predicate-value):
  `drawQuadrille(q, { filter: ({ value }) => brightness(value) < 50 })`

{{< callout type="info" >}}
[Arrow functions](https://www.w3schools.com/js/js_arrow_function.asp) offer a compact syntax. For instance, the predicate

```js
function (cell) {
  return brightness(cell.value) < 50
}
```

becomes:

```js
cell => brightness(cell.value) < 50
```

You can also destructure to focus only on what you need:

```js
({ value }) => brightness(value) < 50
```

{{< /callout >}}

## Example: Filtering by Value Collection

(click on canvas and press any key to randomize `q`)  
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight
let q;                                        // Quadrille
let yellow, blue, red;                        // Colors
let yellowBox, blueBox, redBox;               // Checkboxes
let values = [];                              // Filter array

function setup() {
  createCanvas(600, 400);
  yellow = color('lemonchiffon');
  blue = color('skyblue');
  red = color('tomato');
  // Create quadrille
  q = createQuadrille(30, 20).rand(200, yellow).rand(200, blue).fill(red);
  // Create checkboxes
  yellowBox = createCheckbox('Yellow', true).position(10, 10).changed(update);
  blueBox = createCheckbox('Blue', true).position(10, 30).changed(update);
  redBox = createCheckbox('Red', false).position(10, 50).changed(update);
  // Initialize values array
  update();
}

function draw() {
  background(255);
  // Draw the Quadrille, filtering cells based on checkbox-selected colors
  drawQuadrille(q, { filter: values });
}

function update() {
  values = [];
  yellowBox.checked() && values.push(yellow);
  blueBox.checked() && values.push(blue);
  redBox.checked() && values.push(red);
}

function keyPressed() {
  q.randomize();
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight
let q;                                        // Quadrille
let yellow, blue, red;                        // Colors
let yellowBox, blueBox, redBox;               // Checkboxes
let values = [];                              // Filter array

function setup() {
  createCanvas(600, 400);
  yellow = color('lemonchiffon');
  blue = color('skyblue');
  red = color('tomato');
  // Create quadrille
  q = createQuadrille(30, 20).rand(200, yellow).rand(200, blue).fill(red);
  // Create checkboxes
  yellowBox = createCheckbox('Yellow', true).position(10, 10).changed(update);
  blueBox = createCheckbox('Blue', true).position(10, 30).changed(update);
  redBox = createCheckbox('Red', false).position(10, 50).changed(update);
  // Initialize values array
  update();
}

function draw() {
  background(255);
  // Draw the Quadrille, filtering cells based on checkbox-selected colors
  drawQuadrille(q, { filter: values });
}

function update() {
  values = [];
  yellowBox.checked() && values.push(yellow);
  blueBox.checked() && values.push(blue);
  redBox.checked() && values.push(red);
}

function keyPressed() {
  q.randomize();
}
```
{{% /details %}}

{{< callout type="info" >}}
The `values` array must contain references to the exact instances used to fill the quadrille. For example, if `q` was filled with the variable `yellow`, which holds the value `color('lemonchiffon')`, the `values` array must include the `yellow` variable itself, not a new instance created with `color('lemonchiffon')`.  
{{< /callout >}}

## Example: Filtering by Predicate Value

(click on canvas and press any key to randomize `q`)  
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict'

Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight

let q;                                        // Quadrille
let select;                                   // UI

// Predicate-based color filters
const filters = {
  'All':    undefined,                                // No filter
  'Warm':   ({ value }) => red(value) > blue(value),  // Warmer hues
  'Dark':   ({ value }) => brightness(value) < 50,    // Low brightness
  'Gothic': ({ value }) => saturation(value) < 20 &&
                           brightness(value) < 60     // Muted & dark
};

function setup () {
  createCanvas(600, 400);                    // Create canvas
  q = createQuadrille(30, 20);               // Create quadrille
  // Fill quadrille with random colors using a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  select = createSelect().position(10, 10);  // Dropdown menu
  for (const label in filters) select.option(label); // Populate options
}

function draw () {
  background(255);                           // Clear background
  // Draw filtered quadrille
  drawQuadrille(q, { filter: filters[select.value()] }); 
}

function keyPressed () {
  q.randomize();                             // Randomize on key press
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight

let q;                                        // Quadrille
let select;                                   // UI

// Predicate-based color filters
const filters = {
  'All':    undefined,                                // No filter
  'Warm':   ({ value }) => red(value) > blue(value),  // Warmer hues
  'Dark':   ({ value }) => brightness(value) < 50,    // Low brightness
  'Gothic': ({ value }) => saturation(value) < 20 &&
                           brightness(value) < 60     // Muted & dark
};

function setup () {
  createCanvas(600, 400);                    // Create canvas
  q = createQuadrille(30, 20);               // Create quadrille
  // Fill quadrille with random colors using a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  select = createSelect().position(10, 10);  // Dropdown menu
  for (const label in filters) select.option(label); // Populate options
}

function draw () {
  background(255);                           // Clear background
  // Draw filtered quadrille
  drawQuadrille(q, { filter: filters[select.value()] }); 
}

function keyPressed () {
  q.randomize();                             // Randomize on key press
}
```
{{% /details %}}

{{< callout type="info" >}}
In JavaScript, `for...of` iterates over iterables like arrays, strings, Maps, and Sets, and when used with a quadrille it yields `{ row, col, value }`:

```js
for (const { row, col } of q) {
  q.fill(row, col, color(random(255), random(255), random(255)))
}
```

Destructure only what you need inside predicates (e.g., `{ row, col }`).
{{< /callout >}}

{{< callout type="info" >}}
In JavaScript, `for...in` is used to iterate over *object keys*, typically with plain objects:

```js
for (const label in filters) {
  select.option(label)
}
```
{{< /callout >}}

## Example: Filtering by Predicate Value, Row, and Column

(click on canvas and press any key to randomize `q`)
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict'
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight

const COLS = 30, ROWS = 20;                   // Grid dimensions
let q;                                        // Quadrille
let select;                                   // UI

// Combined cell-predicate filters
const filters = {
  'All':          undefined,                           // No filter
  'Even Rows':    ({ row }) => row % 2 === 0,          // Even rows only
  'Left Half':    ({ col }) => col < COLS / 2,         // Left half only
  'Cool & Right': ({ value, col }) => blue(value) > red(value) && 
                                      col >= COLS / 2, // Cool hues on right half
  'Top Warm':     ({ value, row }) => red(value) > blue(value) &&
                                      row < ROWS / 2   // Warm hues on top half
};

function setup () {
  createCanvas(600, 400);                     // Create canvas
  q = createQuadrille(COLS, ROWS);            // Create quadrille
  // Fill quadrille with random colors using a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  select = createSelect().position(10, 10);   // Dropdown menu
  for (const label in filters) select.option(label); // Populate options
}

function draw () {
  background(255);                            // Clear background
  // Draw filtered quadrille
  drawQuadrille(q, { filter: filters[select.value()] });
}

function keyPressed () {
  q.randomize();                              // Randomize on key press
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight

const COLS = 30, ROWS = 20;                   // Grid dimensions
let q;                                        // Quadrille
let select;                                   // UI

// Combined cell-predicate filters
const filters = {
  'All':          undefined,                           // No filter
  'Even Rows':    ({ row }) => row % 2 === 0,          // Even rows only
  'Left Half':    ({ col }) => col < COLS / 2,         // Left half only
  'Cool & Right': ({ value, col }) => blue(value) > red(value) && 
                                      col >= COLS / 2, // Cool hues on right half
  'Top Warm':     ({ value, row }) => red(value) > blue(value) &&
                                      row < ROWS / 2   // Warm hues on top half
};

function setup () {
  createCanvas(600, 400);                     // Create canvas
  q = createQuadrille(COLS, ROWS);            // Create quadrille
  // Fill quadrille with random colors using a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  select = createSelect().position(10, 10);   // Dropdown menu
  for (const label in filters) select.option(label); // Populate options
}

function draw () {
  background(255);                            // Clear background
  // Draw filtered quadrille
  drawQuadrille(q, { filter: filters[select.value()] });
}

function keyPressed () {
  q.randomize();                              // Randomize on key press
}
```
{{% /details %}}

## Syntax

> `drawQuadrille(quadrille, { filter })`

## Parameters

| Param    | Description                                                                                                                                                                                                                                                                    |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `filter` | Specifies which cells to draw. All cells are drawn if omitted or `undefined`. It can be: <ul><li>a **value collection** (`Array` or `Set`) checked by identity (`===`) against `cell.value`</li><li>a **cell-predicate function** `({ row, col, value }) => boolean`</li></ul> |