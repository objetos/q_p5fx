---
weight: 1
draft: false
title: "createQuadrille()"
---

Creates an 8x8 quadrille with a chessboard pattern.

## Example

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
`use strict`;
// Global style vars
// Quadrille cell length default is: 100, we change it to 50
Quadrille.cellLength = 50;
// Disable the tile display algorithm
Quadrille.tileDisplay = 0;
// quadrille object declaration
let quadrille;

function setup() {
  createCanvas(8 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  // quadrille object initialization
  quadrille = createQuadrille();
}

function draw() {
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// Global style vars
// Quadrille cell length default is: 100, we change it to 50
Quadrille.cellLength = 50;
// Disable the tile display algorithm
Quadrille.tileDisplay = 0;
// quadrille object declaration
let quadrille;

function setup() {
  createCanvas(8 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  // quadrille object initialization
  quadrille = createQuadrille();
}

function draw() {
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
Observe that `createQuadrille()` is equivalent to `createQuadrille(8, 8).fill()`. See [createQuadrille(width, height)]({{< ref "create_quadrille/#createquadrillewidth-height" >}}) and [fill()]({{< ref "fill" >}}).
{{< /callout >}}

## Syntax

> `createQuadrille()`

## Parameters

None.