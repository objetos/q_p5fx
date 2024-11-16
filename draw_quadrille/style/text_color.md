---
weight: 4
draft: false
title: textColor
---

Defines the quadrille default text drawing color. Default is `white`.

Used by [drawQuadrille]({{< ref "draw_quadrille" >}}).

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
Quadrille.textColor = 'magenta';
let quadrille;
let colorPicker;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(5, 'hola mundo');
  colorPicker = createColorPicker(Quadrille.textColor);
  colorPicker.position(width - 60, 10);
  colorPicker.input(() => Quadrille.textColor = colorPicker.value());
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.textColor = 'magenta';
let quadrille;
let colorPicker;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(5, 'hola mundo');
  colorPicker = createColorPicker(Quadrille.textColor);
  colorPicker.position(width - 60, 10);
  colorPicker.input(() => Quadrille.textColor = colorPicker.value());
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## Syntax

> `Quadrille.textColor`