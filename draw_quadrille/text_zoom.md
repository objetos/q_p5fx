---
weight: 8
draft: false
title: textZoom
---

Defines the quadrille default text zoom level. Default is `0.89`

Used by [drawQuadrille]({{< ref "draw_quadrille" >}}).

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.textZoom = 0.5;
let quadrille;
let zoomSlider;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(5, 'hola mundo');
  zoomSlider = createSlider(0.1, 0.9, 0.5, 0.01);
  zoomSlider.position(10, 210);
  zoomSlider.input(() => Quadrille.textZoom = zoomSlider.value());
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.textZoom = 0.5;
let quadrille;
let zoomSlider;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(5, 'hola mundo');
  zoomSlider = createSlider(0.1, 0.9, 0.5, 0.01);
  zoomSlider.position(10, 210);
  zoomSlider.input(() => Quadrille.textZoom = zoomSlider.value());
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## Syntax

> `Quadrille.textColor`