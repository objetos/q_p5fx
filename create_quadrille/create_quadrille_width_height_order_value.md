---
weight: 13
draft: false
title: "createQuadrille(width, height, order, value)"
---

Creates a quadrille of dimensions `width` × `height` and randomly places `value` in exactly `order` cells (clamped to the board size).

## Example

{{< p5 quadrille="true" >}}
'use strict';
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(6, 4, 13, 150);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5 >}}

{{% details title="code" open=true %}}
```js
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(6, 4, 13, 150);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{% /details %}}

{{< callout type="info" >}}
The `order` argument means exactly what the [order]({{< relref "order" >}}) property means — the number of filled cells: after `createQuadrille(6, 4, 13, 150)`, `q.order === 13`. Values beyond the board size clamp: `createQuadrille(2, 2, 99, value)` fills all 4 cells.
{{< /callout >}}

{{< callout type="info" >}}
To define different values in `createQuadrille(width, height, order, value)`, refer to [createQuadrille(jagged_array)]({{< relref "create_quadrille_jagged_array" >}}).
{{< /callout >}}

## Syntax

> `createQuadrille(width, height, order, value)`

## Parameters

| Param  | Description                                                                                                                                        |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `width`  | Number: The total number of columns for the quadrille                                                                                              |
| `height` | Number: The total number of rows for the quadrille                                                                                                |
| `order`  | Number: The number of cells to fill with `value` — the resulting [order]({{< relref "order" >}}) property (clamps to `width × height`)              |
| `value`[^1] | Any: [valid JavaScript value](https://www.w3schools.com/js/js_datatypes.asp), with `null` representing empty cells                       |

[^1]: A plain function `value` is **stored, not called** — it becomes a per-cell display routine `({ row, col, options }) => { ... }` (see [`options`]({{< relref display_fns >}})). To have a function **evaluated per cell** at creation time — a fresh object or a varied tile per cell — tag it: `Quadrille.factory(({ row, col }) => new Object(...))`.