---
weight: 3
draft: false
title: outlineWeight
---

Defines the quadrille default outline weight. Default is `2`.

Used by [drawQuadrille]({{< ref "draw_quadrille" >}}).

## Example

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
`use strict`;
let quadrille;
let weightSlider;

function setup() {
  createCanvas(400, 400);
  quadrille = createQuadrille(4, 4);
  weightSlider = createSlider(1, 10, Quadrille.outlineWeight, 0.5);
  weightSlider.position(10, height - 20);
  weightSlider.input(() => Quadrille.outlineWeight = weightSlider.value());
}

function draw() {
  background('yellow');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let quadrille;
let weightSlider;

function setup() {
  createCanvas(400, 400);
  quadrille = createQuadrille(4, 4);
  weightSlider = createSlider(1, 10, Quadrille.outlineWeight, 0.5);
  weightSlider.position(10, height - 20);
  weightSlider.input(() => Quadrille.outlineWeight = weightSlider.value());
}

function draw() {
  background('yellow');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## Syntax

> `Quadrille.outlineWeight`