---
weight: 9
draft: false
title: filter
---

Filters which cells to draw from a given quadrille `q`. It accepts the following types:

- **A value collection (`Array` or `Set`)**  
  Draws only the cells whose values are included in the collection.  
  [Example](#example-filtering-by-value-collection):  
  `drawQuadrille(q, { filter: [red, blue] })`

- **A predicate function (`function(value): boolean`)**  
  Draws only the cells for which the function returns `true`.  
  [Example](#example-filtering-by-predicate-value):  
  `drawQuadrille(q, { filter: value => brightness(value) < 50 })`

- **An object with optional `value`, `row`, and/or `col` predicate functions**  
  Draws only the cells that match *all* specified predicates.  
  [Example](#example-filtering-by-predicate-value-row-and-column):  
  `drawQuadrille(q, { filter: {value: v => red(v) > 50, row: r => r == 0} })`

{{< callout type="info" >}}  
Arrow functions offer a compact syntax for writing functions. For example, the predicate:

```js
function(value) {
  return brightness(value) < 50;
}
```

can be written more concisely as:

```js
value => brightness(value) < 50
```

Here, the `function` keyword, parentheses (when there’s only one parameter), and the `return` statement (if the body is a single expression) are all omitted.
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
'use strict';
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight

let q;         // Quadrille
let select;    // UI

// Define a set of predicate-based color filters
const filters = {
  'All': undefined,                                       // No filter
  'Warm': c => red(c) > blue(c),                          // Warmer hues
  'Dark': c => brightness(c) < 50,                        // Low brightness
  'Gothic': c => saturation(c) < 20 && brightness(c) < 60 // Muted and dark
};

function setup() {
  createCanvas(600, 400);
  q = createQuadrille(30, 20);
  // Fill quadrille with random colors iterating with a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  select = createSelect().position(10, 10);
  for (const label in filters) {
    select.option(label);
  }
}

function draw() {
  background(255);
  // Draw q with predicate object controlled by the select
  drawQuadrille(q, { filter: filters[select.value()] });
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

let q;               // Quadrilles
let select;          // UI

// Define a set of predicate-based color filters
const filters = {
  'All': undefined,                                       // No filter
  'Warm': c => red(c) > blue(c),                          // Warmer hues
  'Dark': c => brightness(c) < 50,                        // Low brightness
  'Gothic': c => saturation(c) < 20 && brightness(c) < 60 // Muted and dark
};

function setup() {
  createCanvas(600, 400);
  q = createQuadrille(30, 20);
  // Fill quadrille with random colors iterating with a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  select = createSelect().position(10, 10);
  for (const label in filters) {
    select.option(label);
  }
}

function draw() {
  background(255);
  // Draw q with predicate object controlled by the select
  drawQuadrille(q, {filter: filters[select.value()] });
}

function keyPressed() {
  q.randomize();
}
```
{{% /details %}}

{{< callout type="info" >}}  
In JavaScript, `for...of` is used to iterate over *iterables* such as arrays, strings, Maps, Sets, and (custom) generators:

```js
for (const { row, col } of q) {
  q.fill(row, col, color(random(255), random(255), random(255)));
}
```

On the other hand, `for...in` is used to iterate over *object keys*, typically with plain objects:

```js
for (const label in filters) {
  select.option(label);
}
```  
{{< /callout >}}

## Example: Filtering by Predicate Value, Row, and Column

(click on canvas and press any key to randomize `q`)  
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight

const COLS = 30, ROWS = 20;
let q;
let select;

// Object filters combining row/col/value predicates
const filters = {
  'All': undefined,
  'Even Rows': { row: r => r % 2 === 0 },
  'Left Half': { col: c => c < COLS / 2 },
  'Cool & Right': {
    value: c => blue(c) > red(c),
    col: c => c >= COLS / 2
  },
  'Top Warm': {
    value: c => red(c) > blue(c),
    row: r => r < ROWS / 2
  }
};

function setup() {
  createCanvas(600, 400);
  q = createQuadrille(COLS, ROWS);
  // Fill quadrille with random colors using a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  // UI controls
  select = createSelect().position(10, 10);
  for (const label in filters) {
    select.option(label);
  }
}

function draw() {
  background(255);
  drawQuadrille(q, { filter: filters[select.value()] });
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

const COLS = 30, ROWS = 20;
let q;
let select;

// Object filters combining row/col/value predicates
const filters = {
  'All': undefined,
  'Even Rows': { row: r => r % 2 === 0 },
  'Left Half': { col: c => c < COLS / 2 },
  'Cool & Right': {
    value: c => blue(c) > red(c),
    col: c => c >= COLS / 2
  },
  'Top Warm': {
    value: c => red(c) > blue(c),
    row: r => r < ROWS / 2
  }
};

function setup() {
  createCanvas(600, 400);
  q = createQuadrille(COLS, ROWS);
  // Fill quadrille with random colors using a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  // UI controls
  select = createSelect().position(10, 10);
  for (const label in filters) {
    select.option(label);
  }
}

function draw() {
  background(255);
  drawQuadrille(q, { filter: filters[select.value()] });
}

function keyPressed() {
  q.randomize();
}
```
{{% /details %}}

## Syntax

> `drawQuadrille(quadrille, { filter })`

## Parameters

| Param    | Description |
|----------|-------------|
| `filter` | Specifies which cells to draw. All cells are drawn if this parameter is omitted or `undefined`. It can be: <ul><li>a value collection (`Array` or `Set`)</li><li>a predicate function (`value => boolean`)</li><li>an object with optional `value`, `row`, and/or `col` predicates</li></ul> |