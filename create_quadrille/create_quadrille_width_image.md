---
weight: 10
draft: false
title: "createQuadrille(width, image)"
---

Converts an `image` (a [p5.Image](https://p5js.org/reference/#/p5.Image), [p5.Graphics](https://p5js.org/reference/#/p5.Graphics)) or video [p5.MediaElement](https://p5js.org/reference/p5/p5.MediaElement/) into a quadrille with the specified number of columns (`width`), pixelating the image into cells.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="625" >}}
'use strict';
let ps;
let quadrille;

function preload() {
  ps = loadImage('/images/pola.jpg');
}

function setup() {
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
  quadrille = createQuadrille(24, ps);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let ps;
let quadrille;

function preload() {
  ps = loadImage('/images/pola.jpg');
}

function setup() {
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
  quadrille = createQuadrille(24, ps);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
`createQuadrille(width, image)` converts an image into a quadrille, with each cell representing a sub-image.
{{< /callout >}}

## Syntax

> `createQuadrille(width, image)`

## Parameters

| param  | description                                                                                         |
|--------|-----------------------------------------------------------------------------------------------------|
| `width`  | Number: The total number of columns for the quadrille                                               |
| `image`  | [p5.Image](https://p5js.org/reference/#/p5.Image), [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) or video [p5.MediaElement](https://p5js.org/reference/p5/p5.MediaElement/): The image to be pixelated into the quadrille |