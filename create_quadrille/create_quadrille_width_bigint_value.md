---
weight: 12
draft: false
title: "createQuadrille(width, bigint, value)"
---

Converts a [bigint](https://www.w3schools.com/js/js_bigint.asp) into a quadrille pattern, filling the grid cells corresponding to `1` bits in the binary representation of the bigint with the specified `value`. The number of columns is determined by `width`.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
**Observation**\
The `createQuadrille(width, bigint, value)` function creates a quadrille grid based on the binary representation of the bigint. Each `1` bit corresponds to a cell filled with the provided value.
{{< /callout >}}

## Syntax

> `createQuadrille(width, bigint, value)`

## Parameters

| param  | description                                                                                               |
|--------|-----------------------------------------------------------------------------------------------------------|
| width  | Number: The total number of columns for the quadrille.                                                     |
| bigint | BigInt (or Number): A bigint whose binary representation will determine the filled cells in the quadrille. |
| value  | Any: The value used to fill the cells corresponding to `1` bits in the bigint. This can be a color, image, or other valid data type. |