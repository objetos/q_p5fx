---
weight: 13
draft: false
title: "createQuadrille(width, bitboard, value, littleEndian?)"
---

Creates a quadrille by decoding a [bitboard](https://en.wikipedia.org/wiki/Bitboard)—passed as a JavaScript `BigInt`—into a rectangular quadrille. Each bit in the bitboard determines whether a corresponding cell is filled (`1`) or empty (`0`). The number of columns is set by `width`, and rows are inferred as needed.

{{< callout type="info" >}}  
The quadrille [height]({{< relref "height" >}}) is inferred automatically as the minimum number of rows needed to fit all bits in the bitboard, using row-major, big-endian order by default.  
To **explicitly define** the [height]({{< relref "height" >}}), call [`createQuadrille(width, height, bitboard, value[, littleEndian])`]({{< relref "create_quadrille_width_height_bigint_value" >}}).
{{< /callout >}}

## Example 1 — Big-endian (default)

{{< p5-global-iframe quadrille="true" width="325" height="225" >}}
'use strict';
let quadrille;

function setup() {
  createCanvas(300, 200);
  /*
  | 5 | 4 | 3 |
  | 2 | 1 | 0 |
  (0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
  */
  quadrille = createQuadrille(3, 58n, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let quadrille;

function setup() {
  createCanvas(300, 200);
  /*
  | 5 | 4 | 3 |
  | 2 | 1 | 0 |
  (0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
  */
  quadrille = createQuadrille(3, 58n, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{% /details %}}

{{< callout type="info" >}}
This example fills a quadrille using a **bitboard** (`58n` = `0b111010`) in **row-major, big-endian** order:

* **Most significant bit** (2⁵) goes to **(0,0)** (top-left)
* **Least significant bit** (2⁰) goes to **(1,2)** (bottom-right)

```
| 5 | 4 | 3 |
| 2 | 1 | 0 |
(0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
```
{{< /callout >}}

## Example 2 — Little-endian

{{< p5-global-iframe quadrille="true" width="325" height="225" >}}
'use strict';
let quadrille;

function setup() {
  createCanvas(300, 200);
  /*
  | 0 | 1 | 2 |
  | 3 | 4 | 5 |
  (0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
  */
  quadrille = createQuadrille(3, 58n, color('blue'), true); // littleEndian = true
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let quadrille;

function setup() {
  createCanvas(300, 200);
  /*
  | 0 | 1 | 2 |
  | 3 | 4 | 5 |
  (0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
  */
  quadrille = createQuadrille(3, 58n, color('blue'), true); // littleEndian = true
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{% /details %}}

{{< callout type="info" >}}
This example uses the same **bitboard** value (`58n`) but reads it in **row-major, little-endian** order:

* **Least significant bit** (2⁰) goes to **(0,0)** (top-left)
* **Most significant bit** (2⁵) goes to **(1,2)** (bottom-right)

```
| 0 | 1 | 2 |
| 3 | 4 | 5 |
(0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
```

This layout is often used in chess engines such as [Stockfish](https://github.com/official-stockfish/Stockfish), which represent bitboards in little-endian rank-file order.
{{< /callout >}}

{{< callout type="info" >}}
To define different values in `createQuadrille(width, bigint, value)`, refer to [createQuadrille(jagged_array)]({{< relref "create_quadrille_jagged_array" >}}).
{{< /callout >}}

## Syntax

> `createQuadrille(width, bitboard, value[, littleEndian])`

## Parameters

| Param          | Description                                                                                                          |
|----------------|----------------------------------------------------------------------------------------------------------------------|
| `width`        | Number: The total number of columns for the quadrille                                                               |
| `bigint`       | BigInt (or Number): A bigint whose binary representation will determine the filled cells in the quadrille           |
| `value`[^1]    | Any: A [valid JavaScript value](https://www.w3schools.com/js/js_datatypes.asp), with `null` representing empty cells |
| `littleEndian` | Optional Boolean: If `true`, use little-endian bit ordering (default is `false`, i.e., big-endian)                  |

[^1]: If `value` is a function, it is evaluated **per cell**. Use `Quadrille.factory(({ row, col }) => new Object(...))` to generate a new object per cell. For display routines, use a plain function like `({ row, col, options }) => { ... }`. See [`options`]({{< relref display_fns >}}) for available parameters.




