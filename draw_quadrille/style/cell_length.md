---
weight: 1
draft: false
title: cellLength
---

Defines the quadrille default drawing cell length in pixels. Default is `100`.

Used by [drawQuadrille]({{< ref "draw_quadrille" >}}).

## Example

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
`use strict`;
Quadrille.cellLength = 55;
let quadrille;
let lengthSlider;

function setup() {
  createCanvas(400, 400);
  quadrille = createQuadrille(4, 4);
  lengthSlider = createSlider(10, 100, Quadrille.cellLength, 5);
  lengthSlider.position(10, height - 20);
  lengthSlider.input(() => Quadrille.cellLength = lengthSlider.value());
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 55;
let quadrille;
let lengthSlider;

function setup() {
  createCanvas(400, 400);
  quadrille = createQuadrille(4, 4);
  lengthSlider = createSlider(10, 100, Quadrille.cellLength, 5);
  lengthSlider.position(10, height - 20);
  lengthSlider.input(() => Quadrille.cellLength = lengthSlider.value());
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## Syntax

> `Quadrille.cellLength`