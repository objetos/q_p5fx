---
weight: 11
draft: false  
title: origin
---

`origin` define the origin where to draw a given quadrille; it can be `CORNER` or `CENTER`; default is `CORNER` in `P2D` and `CENTER` in `WEBGL` mode.

## Example

(click or press any key to define `q` `origin` either as `CORNER` or `CENTER`)\
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
// q0 is the reference quadrille
let q0, q;
let center = false;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58, color('blue'));
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
  q = createQuadrille(3, 58, color('blue'));
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

| Param    | Description                                                   |
|----------|---------------------------------------------------------------|
| `origin` |   |