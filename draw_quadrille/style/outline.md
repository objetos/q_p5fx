---
weight: 2
draft: false
title: outline
---

Defines the quadrille default text drawing color. Default is `grey`.

Used by [drawQuadrille]({{< ref "draw_quadrille" >}}).

## Example

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
'use strict';
Quadrille.outline = 'cyan';
let quadrille;
let colorPicker;

function setup() {
  createCanvas(400, 400);
  quadrille = createQuadrille(4, 4);
  colorPicker = createColorPicker(Quadrille.outline);
  colorPicker.position(width - 60, 10);
  colorPicker.input(() => Quadrille.outline = colorPicker.value());
}

function draw() {
  background('red');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.outline = 'cyan';
let quadrille;
let colorPicker;

function setup() {
  createCanvas(400, 400);
  quadrille = createQuadrille(4, 4);
  colorPicker = createColorPicker(Quadrille.outline);
  colorPicker.position(width - 60, 10);
  colorPicker.input(() => Quadrille.outline = colorPicker.value());
}

function draw() {
  background('red');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## Syntax

> `Quadrille.outline`