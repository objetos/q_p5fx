---
weight: 9
draft: false
title: "createQuadrille(width, string)"
---

Creates a quadrille and fills its cells using the characters from the provided `string`. The number of columns is defined by `width`, and the characters are arranged across multiple rows if necessary.

## Example

{{< p5-global-iframe quadrille="true" width="425" height="225" >}}
'use strict';
let quadrille;

function setup() {
  createCanvas(4 * Quadrille.cellLength, 2 * Quadrille.cellLength);
  quadrille = createQuadrille(4, 'hola 👾👽!');
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
  createCanvas(4 * Quadrille.cellLength, 2 * Quadrille.cellLength);
  quadrille = createQuadrille(4, 'hola 👽!');
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{% /details %}}

{{< callout type="info" >}}
The `createQuadrille(width, string)` function allows you to control the number of columns (`width`) while filling the quadrille with the characters from the provided `string`. Characters will automatically overflow into additional rows as needed.
{{< /callout >}}

## Syntax

> `createQuadrille(width, string)`

## Parameters

| Param    | Description                                                    |
|----------|----------------------------------------------------------------|
| `width`  | Number: The total number of columns for the quadrille          |
| `string` | String: The string used to fill the quadrille cells. Each character occupies one cell |