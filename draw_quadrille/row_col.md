---
weight: 8
draft: false  
title: row & col  
---

The `row` and `col` parameters define the position of the upper-left corner where the quadrille is drawn, in row and column units.

## Example

(move the mouse to position `q`)
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
// q0 is the reference quadrille
let q0, q;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  drawQuadrille(q, { row: q0.mouseRow, col: q0.mouseCol, outline: 'lime' });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// q0 is the reference quadrille
let q0, q;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  drawQuadrille(q, { row: q0.mouseRow, col: q0.mouseCol, outline: 'lime' });
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
The [mouseRow]({{< ref "mouse_row" >}}) and [mouseCol]({{< ref "mouse_col" >}}) Quadrille properties are used to dynamically position the `q` quadrille based on the mouse location.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, { row, col })`

## Parameters

| Param | Description                                                   |
|-------|---------------------------------------------------------------|
| `row` | Number: The row position of the upper-left corner in units    |
| `col` | Number: The column position of the upper-left corner in units |