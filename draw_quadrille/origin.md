---
weight: 11  
draft: false  
title: origin  
---

The `origin` parameter defines the top-left corner of the quadrille for drawing: `CORNER` positions it at the top-left corner of the canvas, the default in `P2D`; `CENTER` positions it at the center of the canvas, the default in `WEBGL`.

## Example

(click or press any key to toggle the origin of `q` between `CORNER` and `CENTER`)\
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
// q0 is the reference quadrille
let q0, q;
let center = false;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58n, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  drawQuadrille(q, { origin: center ? CENTER : CORNER });
}

function mouseClicked() {
  center = !center;
}

function keyPressed() {
  center = !center;
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// q0 is the reference quadrille
let q0, q;
let center = false;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58n, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  drawQuadrille(q, { origin: center ? CENTER : CORNER });
}

function mouseClicked() {
  center = !center;
}

function keyPressed() {
  center = !center;
}
```
{{< /details >}}

## Syntax

> `drawQuadrille(quadrille, { origin })`

## Parameters

| Param  | Description                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| origin | Constant: `CORNER` draws the quadrille aligned to the top-left corner of the canvas (default in `P2D`); `CENTER` draws it aligned to the center of the canvas (default in `WEBGL`) |