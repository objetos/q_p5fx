---
weight: 11
draft: false
title: "createQuadrille(width, image, coherence)"
---

Converts an `image` (either a [p5.Image](https://p5js.org/reference/#/p5.Image) or a [p5.Graphics](https://p5js.org/reference/#/p5.Graphics)) into a pixelated quadrille. The `coherence` parameter defines whether or not to use spatial coherence while filling the quadrille grid cells.

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
  quadrille = createQuadrille(24, sb, false);
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
  quadrille = createQuadrille(24, sb, false);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
The `createQuadrille(width, image, coherence)` function converts an image into a pixelated quadrille grid, where the `coherence` parameter determines whether the spatial coherence of the image should be preserved.
{{< /callout >}}

## Syntax

> `createQuadrille(width, image, coherence)`

## Parameters

| param     | description                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| width     | Number: The total number of columns for the quadrille.                                               |
| image     | [p5.Image](https://p5js.org/reference/#/p5.Image) or [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): The image to be pixelated into the quadrille. |
| coherence | Boolean: Defines whether to preserve spatial coherence when converting the image. Default is `false`. |