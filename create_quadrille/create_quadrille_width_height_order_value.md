---
weight: 12
draft: false
title: "createQuadrille(width, height, order, value)"
---

Creates a quadrille and fills its cells using the specified `value`, which is randomly repeated throughout the quadrille up to `order` number of times. The dimensions of the quadrille are determined by `width` and `height`.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(4, 3, 7, 150);
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
  quadrille = createQuadrille(4, 3, 7, 150);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\ 
`createQuadrille(width, height, order, value)` fills a quadrille with the given value, distributing it randomly up to the specified `order` count.
{{< /callout >}}

## Syntax

> `createQuadrille(width, height, order, value)`

## Parameters

| param  | description                                                                                                                                        |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| width  | Number: The total number of columns for the quadrille.                                                                                              |
| height | Number: The total number of rows for the quadrille.                                                                                                |
| order  | Number: The number of non-empty cells to be filled with the `value`.                                                                                |
| value  | Any: The value to be used to fill the quadrille cells. This can be an image, color, string, number, or other valid data type.                       |