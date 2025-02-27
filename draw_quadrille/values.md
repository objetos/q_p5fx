---
weight: 9
draft: false
title: values
---

Selectively draws cells in the `quadrille` based on the specified `values`, and skips tiles of unselected cells. This feature is often paired with a reference quadrille used to define the tiles.

## Example

(click on canvas and press any key to randomize `q`)\
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 20;
Quadrille.outlineWeight = 1;
Quadrille.outline = '#101010';
// Reference quadrille (tile) used for tile display
let tile, q;
let yellow, blue, red;
let yellowBox, blueBox, redBox, tileBox;
let values = [];

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
  tileBox = createCheckbox('Toggle tile', true).position(10, 70);
  // Initialize values array
  update();
}

function draw() {
  background(255);
  // Draw q with values controlled by checkboxes
  drawQuadrille(q, { tileDisplay: 0, values });
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
Quadrille.cellLength = 20;
Quadrille.outlineWeight = 1;
Quadrille.outline = '#101010';
// Reference quadrille (tile) used for tile display
let tile, q;
let yellow, blue, red;
let yellowBox, blueBox, redBox, tileBox;
let values = [];

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
  tileBox = createCheckbox('Toggle tile', true).position(10, 70);
  // Initialize values array
  update();
}

function draw() {
  background(255);
  // Draw q with values controlled by checkboxes
  drawQuadrille(q, { tileDisplay: 0, values });
  // Optionally draw tile for tile display
  tileBox.checked() && drawQuadrille(tile);
}

function update() {
  values = [];
  yellowBox.checked() && values.push(yellow);
  blueBox.checked() && values.push(blue);
  redBox.checked() && values.push(red);
}

function mousePressed() {
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

## Syntax

> `drawQuadrille(quadrille, { values })`

## Parameters

| Param    | Description                                                                                 |
|----------|---------------------------------------------------------------------------------------------|
| `values` | [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): Specifies which cells to draw; tiles of unselected cells are skipped. All cells are drawn if this parameter is `undefined` |