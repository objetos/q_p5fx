---
weight: 9
draft: false
title: filter
---

Selectively draws cells in the `quadrille` based on the specified `filter`, and skips tiles of unselected cells. This feature is often paired with a reference quadrille used to define the tiles.

## Example: Arrays

(click on canvas and press any key to randomize `q`)  
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight

let tile, q;                                  // Quadrilles

let yellow, blue, red;                        // Colors
let yellowBox, blueBox, redBox, tileBox;      // Checkboxes
let values = [];                              // Filter array

function setup() {
  createCanvas(600, 400);
  yellow = color('lemonchiffon');
  red = color('tomato');
  blue = color('skyblue');
  // Create quadrilles
  tile = createQuadrille(30, 20);
  q = createQuadrille(30, 20).rand(200, yellow).rand(200, blue).fill(red);
  // Create checkboxes
  yellowBox = createCheckbox('Yellow', true).position(10, 10).changed(update);
  blueBox = createCheckbox('Blue', true).position(10, 30).changed(update);
  redBox = createCheckbox('Red', false).position(10, 50).changed(update);
  tileBox = createCheckbox('Toggle tile', true).position(width - 100, 10);
  // Initialize values array
  update();
}

function draw() {
  background(255);
  // Draw q with array of color values controlled by checkboxes
  drawQuadrille(q, { tileDisplay: 0, filter: values });
  // Optionally draw tile for tile display
  tileBox.checked() && drawQuadrille(tile);
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

let tile, q;                                  // Quadrilles

let yellow, blue, red;                        // Colors
let yellowBox, blueBox, redBox, tileBox;      // Checkboxes
let values = [];                              // Filter array

function setup() {
  createCanvas(600, 400);
  yellow = color('lemonchiffon');
  red = color('tomato');
  blue = color('skyblue');
  // Create quadrilles
  tile = createQuadrille(30, 20);
  q = createQuadrille(30, 20).rand(200, yellow).rand(200, blue).fill(red);
  // Create checkboxes
  yellowBox = createCheckbox('Yellow', true).position(10, 10).changed(update);
  blueBox = createCheckbox('Blue', true).position(10, 30).changed(update);
  redBox = createCheckbox('Red', false).position(10, 50).changed(update);
  tileBox = createCheckbox('Toggle tile', true).position(width - 100, 10);
  // Initialize values array
  update();
}

function draw() {
  background(255);
  // Draw q with array of color values controlled by checkboxes
  drawQuadrille(q, { tileDisplay: 0, filter: values });
  // Optionally draw tile for tile display
  tileBox.checked() && drawQuadrille(tile);
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

{{< callout type="info" >}}  
The `&&` operator in the `update()` function acts as a [short-circuiting conditional](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND). If the condition before `&&` is true (e.g., `yellowBox.checked()`), the expression after `&&` (e.g., `values.push(yellow)`) is executed. This makes the code concise and avoids the need for `if` statements.  
For example:  
```js
yellowBox.checked() && values.push(yellow);
```  
is equivalent to:  
```js
if (yellowBox.checked()) {
  values.push(yellow);
}
```  
{{< /callout >}}

## Example: Predicates

(click on canvas and press any key to randomize `q`)  
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight

let q, tile;         // Quadrilles
let tileBox, select; // UI

// Define a set of predicate-based color filters
const filters = {
  'All': undefined,                                       // No filter: show all
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
  tile = createQuadrille(30, 20);
  tileBox = createCheckbox('Toggle tile', true).position(width - 100, 10);
  select = createSelect().position(10, 10);
  for (const label in filters) {
    select.option(label);
  }
}

function draw() {
  background(255);
  // Draw q with predicate object controlled by the select
  drawQuadrille(q, { tileDisplay: 0, filter: filters[select.value()] });
  tileBox.checked() && drawQuadrille(tile);
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

let q, tile;         // Quadrilles
let tileBox, select; // UI

// Define a set of predicate-based color filters
const filters = {
  'All': undefined,                                       // No filter: show all
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
  tile = createQuadrille(30, 20);
  tileBox = createCheckbox('Toggle tile', true).position(width - 100, 10);
  select = createSelect().position(10, 10);
  for (const label in filters) {
    select.option(label);
  }
}

function draw() {
  background(255);
  // Draw q with predicate object controlled by the select
  drawQuadrille(q, { tileDisplay: 0, filter: filters[select.value()] });
  tileBox.checked() && drawQuadrille(tile);
}

function keyPressed() {
  q.randomize();
}
```
{{% /details %}}

## Example: Object with optional `value`, `row`, and/or `col` predicates

(click on canvas and press any key to randomize `q`)  
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 20;                    // Set cell size
Quadrille.outline = '#FF00FF';                // Set outline color
Quadrille.outlineWeight = 1;                  // Set outline weight

const COLS = 30, ROWS = 20;
let q, tile
let tileBox, select;

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
  tile = createQuadrille(COLS, ROWS);
  // Fill quadrille with random colors using a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  // UI controls
  tileBox = createCheckbox('Toggle tile', true).position(width - 100, 10);
  select = createSelect().position(10, 10);
  for (const label in filters) {
    select.option(label);
  }
}

function draw() {
  background(255);
  drawQuadrille(q, { tileDisplay: 0, filter: filters[select.value()] });
  tileBox.checked() && drawQuadrille(tile);
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
let q, tile;
let tileBox, select;

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
  tile = createQuadrille(COLS, ROWS);
  // Fill quadrille with random colors using a for...of loop
  for (const { row, col } of q) {
    q.fill(row, col, color(random(255), random(255), random(255)));
  }
  // UI controls
  tileBox = createCheckbox('Toggle tile', true).position(width - 100, 10);
  select = createSelect().position(10, 10);
  for (const label in filters) {
    select.option(label);
  }
}

function draw() {
  background(255);
  drawQuadrille(q, { tileDisplay: 0, filter: filters[select.value()] });
  tileBox.checked() && drawQuadrille(tile);
}

function keyPressed() {
  q.randomize();
}
```
{{% /details %}}

## Syntax

> `drawQuadrille(quadrille, { filter })`

## Parameters

| Param    | Description                                                                                 |
|----------|---------------------------------------------------------------------------------------------|
| `filter` | [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): Specifies which cells to draw; tiles of unselected cells are skipped. All cells are drawn if this parameter is `undefined` |