---
weight: 2
draft: false
title: "createQuadrille(color1, color2)"
---

Creates an 8x8 quadrille with a chessboard pattern.

## Example

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
'use strict';
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
  quadrille = createQuadrille('lime', 'magenta');
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
  quadrille = createQuadrille('lime', 'magenta');
}

function draw() {
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
Observe that `createQuadrille(color1, color2)` is equivalent to `createQuadrille(8, 8).fill(color1, color2)`. See [createQuadrille(width, height)]({{< ref "create_quadrille/#createquadrillewidth-height" >}}) and [fill(color1, color2)]({{< ref "fill_color_color" >}}).
{{< /callout >}}

## Syntax

> `createQuadrille(color1, color2)`

## Parameters

| Param  | Description                                                                                             |
|--------|---------------------------------------------------------------------------------------------------------|
| `color1` | [p5.Color](https://p5js.org/reference/#/p5.Color) \| String: The color used for the light squares of the chessboard pattern. Can be a `p5.Color` instance or an HTML color string (e.g., `'red'`, `'#ff0000'`, `'rgb(255,0,0)'`) |
| `color2` | [p5.Color](https://p5js.org/reference/#/p5.Color) \| String: The color used for the dark squares of the chessboard pattern. Can be a `p5.Color` instance or an HTML color string                                                |
