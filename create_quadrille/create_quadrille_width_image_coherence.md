---
weight: 11  
draft: false  
title: "createQuadrille(width, image, coherence)"  
---

Converts an `image` (a [p5.Image](https://p5js.org/reference/#/p5.Image), [p5.Graphics](https://p5js.org/reference/#/p5.Graphics), or a video [p5.MediaElement](https://p5js.org/reference/p5/p5.MediaElement/)) into a pixelated quadrille. The `coherence` parameter **must be provided** to control spatial coherence; omitting it invokes [createQuadrille(width, image)]({{< relref "create_quadrille_width_image" >}}).

## Example

{{< p5-global-iframe quadrille="true" width="625" height="625" >}}
'use strict';
let ps;
let quadrille;
let coherence;

function preload() {
  ps = loadImage('/images/pola.jpg');
}

function setup() {
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
  // Initialize checkbox with a label
  coherence = createCheckbox('Coherence', false)
    .position(10, 10)
    .style('color', 'white')
    .changed(update);
  // Initial quadrille setup
  update();
}

function update() {
  // Toggle coherence based on checkbox state
  quadrille = createQuadrille(24, ps, coherence.checked());
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let ps;
let quadrille;
let coherence;

function preload() {
  ps = loadImage('/images/pola.jpg');
}

function setup() {
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
  // Initialize checkbox with a label
  coherence = createCheckbox('Coherence', false)
    .position(10, 10)
    .style('color', 'white')
    .changed(update);
  // Initial quadrille setup
  update();
}

function update() {
  // Toggle coherence based on checkbox state
  quadrille = createQuadrille(24, ps, coherence.checked());
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{% /details %}}

## Syntax

> `createQuadrille(width, image, coherence)`

## Parameters

| Param       | Description                                                                                         |
|-------------|-----------------------------------------------------------------------------------------------------|
| `width`     | Number: The total number of columns for the quadrille                                               |
| `image`     | [p5.Image](https://p5js.org/reference/#/p5.Image), [p5.Graphics](https://p5js.org/reference/#/p5.Graphics), or [p5.MediaElement](https://p5js.org/reference/p5/p5.MediaElement/): The image to be pixelated into the quadrille |
| `coherence` | Boolean: Defines whether to preserve spatial coherence when converting the image. **Required**      |