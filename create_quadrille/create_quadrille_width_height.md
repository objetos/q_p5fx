---
weight: 3
draft: false
title: "createQuadrille(width, height)"
---

Creates an empty quadrille having `width` number of columns and `height` number of rows.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
// quadrille object declaration
let quadrille;

function setup() {
  // Quadrille.cellLength is a constant defining the quadrille
  // cell length default is: 100
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // quadrille object initialization
  quadrille = createQuadrille(4, 3);
}

function draw() {
  background('violet');
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// quadrille object declaration
let quadrille;

function setup() {
  // Quadrille.cellLength is a constant defining the quadrille
  // cell length default is: 100
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // quadrille object initialization
  quadrille = createQuadrille(4, 3);
}

function draw() {
  background('violet');
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
`createQuadrille(width, height)` creates an empty grid with the specified dimensions. See also [fill()]({{< ref "fill" >}}) for populating the quadrille.
{{< /callout >}}

## Syntax

> `createQuadrille(width, height)`

## Parameters

| param  | description                       |
|--------|-----------------------------------|
| width  | Number: total number of columns   |
| height | Number: total number of rows      |