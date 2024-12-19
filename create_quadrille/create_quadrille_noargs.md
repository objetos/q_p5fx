---
weight: 1  
draft: false  
title: "createQuadrille()"  
---

Creates an 8x8 quadrille with a chessboard pattern.

## Example

{{< p5-global-iframe quadrille="true" width="670" height="345" >}}
'use strict';
// Set the cell length for all quadrilles (default is 100, changed to 40 here)
Quadrille.cellLength = 40;
// Disable the tile display algorithm for all Quadrille objects
Quadrille.tileDisplay = 0;
let q1, q2;

function setup() {
  createCanvas(16 * Quadrille.cellLength + 10, 8 * Quadrille.cellLength);
  // Instantiate two quadrille objects
  q1 = createQuadrille();
  // Update global square colors for all new Quadrille objects
  Quadrille.lightSquare = '#EBECCF'; // chess.com light square color
  Quadrille.darkSquare = '#769555'; // chess.com dark square color
  q2 = createQuadrille();
}

function draw() {
  // Display q1
  drawQuadrille(q1);
  // Display q2 with an x-offset of 330 pixels
  drawQuadrille(q2, { x: 330 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// Set the cell length for all quadrilles (default is 100, changed to 40 here)
Quadrille.cellLength = 40;
// Disable the tile display algorithm for all Quadrille objects
Quadrille.tileDisplay = 0;
let q1, q2;

function setup() {
  createCanvas(16 * Quadrille.cellLength + 10, 8 * Quadrille.cellLength);
  // Instantiate two quadrille objects
  q1 = createQuadrille();
  // Update global square colors for all new Quadrille objects
  Quadrille.lightSquare = '#EBECCF'; // chess.com light square color
  Quadrille.darkSquare = '#769555'; // chess.com dark square color
  q2 = createQuadrille();
}

function draw() {
  // Display q1
  drawQuadrille(q1);
  // Display q2 with an x-offset of 330 pixels
  drawQuadrille(q2, { x: 330 });
}
```
{{< /details >}}

{{< callout type="info" >}}
`createQuadrille()` is equivalent to `createQuadrille(8, 8).fill()`. See [createQuadrille(width, height)]({{< ref "create_quadrille/#createquadrillewidth-height" >}}) and [fill()]({{< ref "fill" >}}).
{{< /callout >}}

{{< callout type="warning" >}}
**Global Parameters**  
The following parameters are static fields of the `Quadrille` class, meaning they are shared across all instances of `Quadrille`. Changing these values affects all newly created quadrille objects:
- `Quadrille.lightSquare` and `Quadrille.darkSquare`: Define the colors for the light and dark squares of the chessboard pattern.
- [Quadrille.cellLength]({{< ref "cell_length" >}}) and [Quadrille.tileDisplay]({{< ref "display_fns" >}}) are discussed separately.
{{< /callout >}}

## Syntax

> `createQuadrille()`

## Parameters

| Param                 | Description                                                                                             |
|-----------------------|---------------------------------------------------------------------------------------------------------|
| `Quadrille.lightSquare` | String \| [p5.Color](https://p5js.org/reference/#/p5.Color): The global color used for the light squares of the chessboard pattern. Can be an HTML color string (e.g., `'red'`, `'#ff0000'`, `'rgb(255,0,0)'`) or a `p5.Color` instance. Default is `#FDCDAA` |
| `Quadrille.darkSquare`  | String \| [p5.Color](https://p5js.org/reference/#/p5.Color): The global color used for the dark squares of the chessboard pattern. Can be an HTML color string or a `p5.Color` instance. Default is `#D28C45` |