---
weight: 9
draft: false
title: values
---

Selectively draws cells in the `quadrille` with specified `values`, also discarding tile of unselected cells.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 20;
// q0 is defined as reference quadrille and use to draw tile
let q0, q1;
let yellow, blue, red;

function setup() {
  createCanvas(600, 400);
  yellow = color('yellow');
  red = color('red');
  blue = color('blue');
  q0 = createQuadrille(30, 20);
  q1 = createQuadrille(30, 20).rand(200, yellow).rand(200, blue).fill(red);
}

function draw() {
  background(0);
  drawQuadrille(q1, { tileDisplay: 0, values: [yellow, blue] });
  drawQuadrille(q0, { outlineWeight: 1 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 20;
// q0 is defined as reference quadrille
let q0, q1;
let yellow, blue, red;

function setup() {
  createCanvas(600, 400);
  yellow = color('yellow');
  red = color('red');
  blue = color('blue');
  q0 = createQuadrille(30, 20);
  q1 = createQuadrille(30, 20).rand(200, yellow).rand(200, blue).fill(red);
}

function draw() {
  background(0);
  drawQuadrille(q1, { tileDisplay: 0, values: [yellow, blue] });
  drawQuadrille(q0, { outlineWeight: 1 });
}
```
{{< /details >}}

## Syntax

> `drawQuadrille(quadrille, { values })`

## Parameters

| Param  | Description                                                                                 |
|--------|---------------------------------------------------------------------------------------------|
| values | [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): Cells to draw; all cells are drawn if this parameter is `undefined` |