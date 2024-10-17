---
weight: 9
draft: false
title: "createQuadrille(width, image)"
---

Converts an `image` (either a [p5.Image](https://p5js.org/reference/#/p5.Image) or a [p5.Graphics](https://p5js.org/reference/#/p5.Graphics)) into a quadrille with the specified number of columns (`width`). The image is pixelated into the quadrille grid cells.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="625" >}}
`use strict`;
let sb;
let quadrille;

function preload() {
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
  quadrille = createQuadrille(24, sb);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let sb;
let quadrille;

function preload() {
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
  quadrille = createQuadrille(24, sb);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
The `createQuadrille(width, image)` function converts an image into a quadrille grid, where each cell represents a pixel from the image.
{{< /callout >}}

## Syntax

> `createQuadrille(width, image)`

## Parameters

| param  | description                                                                                         |
|--------|-----------------------------------------------------------------------------------------------------|
| width  | Number: The total number of columns for the quadrille.                                               |
| image  | [p5.Image](https://p5js.org/reference/#/p5.Image) or [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): The image to be pixelated into the quadrille. |