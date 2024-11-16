---
weight: 1
draft: false
title: "createQuadrille()"
---

Creates an 8x8 quadrille with a chessboard pattern.

## Example

{{< p5-global-iframe quadrille="true" width="665" height="340" >}}
`use strict`;
// Global style vars
// Quadrille cell length default is: 100, we change it to 40
Quadrille.cellLength = 40;
// Disable the tile display algorithm
Quadrille.tileDisplay = 0;
// quadrille object declaration
let q1, q2;

function setup() {
  createCanvas(17 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  // quadrille object instantiation
  q1 = createQuadrille();
  // Global white and black square colors used from now on
  Quadrille.whiteSquare = '#769555';
  Quadrille.blackSquare = '#EBECCF';
  q2 = createQuadrille();
}

function draw() {
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(q1);
  drawQuadrille(q2, { x: 330, y: 0 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// Global style vars
// Quadrille cell length default is: 100, we change it to 40
Quadrille.cellLength = 40;
// Disable the tile display algorithm
Quadrille.tileDisplay = 0;
// quadrille object declaration
let q1, q2;

function setup() {
  createCanvas(17 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  // quadrille object instantiation
  q1 = createQuadrille();
  // Global white and black square colors used from now on
  Quadrille.whiteSquare = '#769555';
  Quadrille.blackSquare = '#EBECCF';
  q2 = createQuadrille();
}

function draw() {
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(q1);
  drawQuadrille(q2, { x: 330, y: 0 });
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

| param | description                                                                                   |
|-------|-----------------------------------------------------------------------------------------------|
| Quadrille.whiteSquare | [p5.Color](https://p5js.org/reference/#/p5.Color) \| String: The global color used for the white squares of the chessboard pattern. Can be a `p5.Color` instance or an HTML color string (e.g., `'red'`, `'#ff0000'`, `'rgb(255,0,0)'`). Default is `#FDCDAA` |
| Quadrille.blackSquare | [p5.Color](https://p5js.org/reference/#/p5.Color) \| String: The global color used for the black squares of the chessboard pattern. Can be a `p5.Color` instance or an HTML color string. Default is `#D28C45` |