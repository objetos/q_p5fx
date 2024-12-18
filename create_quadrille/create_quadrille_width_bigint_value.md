---
weight: 13
draft: false
title: "createQuadrille(width, bigint, value)"
---

Converts a [bigint](https://www.w3schools.com/js/js_bigint.asp) to a quadrille, filling cells corresponding to `1` bits in the bigint's binary representation with the given `value`. The number of columns is set by `width`.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 200;
let quadrille;

function setup() {
  createCanvas(600, 400);
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

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 200;
let quadrille;

function setup() {
  createCanvas(600, 400);
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
{{< /details >}}

{{< callout type="info" >}}  
This example uses a [bitboard](https://en.wikipedia.org/wiki/Bitboard) to fill the quadrille. The binary form of `58` is `111010`, where each bit corresponds to a cell in the quadrille:  
- A **1** bit means the cell is filled.  
- A **0** bit means the cell is empty.  
The bits are read from bottom to top and left to right, as shown below:  
```
| 5 | 4 | 3 |
| 2 | 1 | 0 |
(0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
```
{{< /callout >}}

{{< callout type="info" >}}
To define different values in `createQuadrille(width, bigint, value)`, refer to [createQuadrille(jagged_array)]({{< relref "create_quadrille_jagged_array" >}}).
{{< /callout >}}

## Syntax

> `createQuadrille(width, bigint, value)`

## Parameters

| param  | description                                                                                               |
|--------|-----------------------------------------------------------------------------------------------------------|
| `width`  | Number: The total number of columns for the quadrille                                                     |
| `bigint` | BigInt (or Number): A bigint whose binary representation will determine the filled cells in the quadrille |
| `value`  | Any: [valid JavaScript value](https://www.w3schools.com/js/js_datatypes.asp), with `null` representing empty cells |