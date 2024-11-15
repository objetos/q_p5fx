---
weight: 9
draft: false
title: "createQuadrille(width, string)"
---

Creates a quadrille and fills its cells using the characters from the provided `string`. The number of columns is defined by `width`, and the characters are arranged across multiple rows if necessary.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(2, 'hi 👽');
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
  quadrille = createQuadrille(2, 'hi 👽');
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
The `createQuadrille(width, string)` function allows you to control the number of columns (`width`) while filling the quadrille with the characters from the provided `string`. Characters will automatically overflow into additional rows as needed.
{{< /callout >}}

## Syntax

> `createQuadrille(width, string)`

## Parameters

| param  | description                                                    |
|--------|----------------------------------------------------------------|
| width  | Number: The total number of columns for the quadrille.          |
| string | String: The string used to fill the quadrille cells. Each character occupies one cell. |