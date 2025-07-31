---
weight: 12
draft: false
title: "createQuadrille(width, height, predicate, value)"
---

Creates a quadrille of the specified size and fills each cell **only if** the given `predicate({ row, col })` returns true. The filled cells are assigned the provided `value`.

This method is ideal for generating patterns like diagonals, borders, checkerboards, or any logical layout based on cell position.

## Example

(fill the two diagonals with 🌀 symbols)  
{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
'use strict';
Quadrille.cellLength = 50;
let q;

function setup() {
  createCanvas(8 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  q = createQuadrille(8, 8, ({ row, col }) => row === col || row + col === 7, '🌀');
}

function draw() {
  background('beige');
  drawQuadrille(q);
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
Quadrille.cellLength = 50;
let q;

function setup() {
  createCanvas(8 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  q = createQuadrille(8, 8, ({ row, col }) => row === col || row + col === 7, '🌀');
}

function draw() {
  background('beige');
  drawQuadrille(q);
}
```
{{% /details %}}

## Syntax

> `createQuadrille(width, height, predicate, value)`

## Parameters

| Param       | Description                                                                       |
| ----------- | --------------------------------------------------------------------------------- |
| `width`     | Number: total number of columns in the quadrille                                  |
| `height`    | Number: total number of rows in the quadrille                                     |
| `predicate` | Function: receives `{ row, col }` and returns `true` if the cell should be filled |
| `value`[^1] | Any: the value to assign to matching cells. Can be a literal, function, or object |

[^1]: If `value` is a function, it is evaluated **per cell**. Use `Quadrille.factory(({ row, col }) => new Object(...))` to generate a new object per cell. For display routines, use a plain function like `({ row, col, options }) => { ... }`. See [`options`]({{< relref display_fns >}}) for available parameters.