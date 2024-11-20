---
weight: 9
draft: false
title: values
---

Selectively draws cells in the `quadrille` with specified `values`, also discarding tile of unselected cells.

## Example

(click on canvas and press any key to randomize `q`)\
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 20;
Quadrille.outlineWeight = 1;
Quadrille.outline = '#101010';
// tile quadrille is defined as a reference quadrille and used to draw tiles
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

keyPressed = () => q.randomize();
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 20;
Quadrille.outlineWeight = 1;
Quadrille.outline = '#101010';
// tile quadrille is defined as a reference quadrille and used to draw tiles
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

keyPressed = () => q.randomize();
```
{{< /details >}}

## Syntax

> `drawQuadrille(quadrille, { values })`

## Parameters

| Param  | Description                                                                                 |
|--------|---------------------------------------------------------------------------------------------|
| values | [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): Cells to draw; all cells are drawn if this parameter is `undefined` |