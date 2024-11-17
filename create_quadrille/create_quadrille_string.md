---
weight: 8
draft: false
title: "createQuadrille(string)"
---

Creates a quadrille and fills its cells using the characters from the provided `string`. The number of columns in the quadrille matches the length of the string.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille('hi 👽');
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
  quadrille = createQuadrille('hi 👽');
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
The `createQuadrille(string)` function fills a quadrille with each character of the provided string, where each column represents one character.
{{< /callout >}}

## Syntax

> `createQuadrille(string)`

## Parameters

| param  | description                                                    |
|--------|----------------------------------------------------------------|
| string | String: The string used to fill the quadrille cells. Each character occupies one cell. |