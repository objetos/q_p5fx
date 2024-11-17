---
weight: 13
draft: false
title: "createQuadrille(width, bigint, value)"
---

Converts a [bigint](https://www.w3schools.com/js/js_bigint.asp) to a quadrille, filling cells corresponding to `1` bits in the bigint's binary representation with the given `value`. The number of columns is set by `width`.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
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
`createQuadrille(width, bigint, value)` generates a quadrille from the bigint's binary representation. Each `1` bit fills a cell with the specified value.
{{< /callout >}}

## Syntax

> `createQuadrille(width, bigint, value)`

## Parameters

| param  | description                                                                                               |
|--------|-----------------------------------------------------------------------------------------------------------|
| width  | Number: The total number of columns for the quadrille.                                                     |
| bigint | BigInt (or Number): A bigint whose binary representation will determine the filled cells in the quadrille. |
| value  | Any: The value used to fill the cells corresponding to `1` bits in the bigint. This can be a color, image, or other valid data type. |