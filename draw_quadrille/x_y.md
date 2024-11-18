---
weight: 2  
draft: false  
title: x & y  
---

The `x` and `y` parameters define the upper-left corner where the quadrille is drawn, in pixels.

## Example

(move the mouse to position `q`)\
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
// q0 is the reference quadrille
let q0, q;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  drawQuadrille(q, { x: mouseX, y: mouseY, outline: 'lime' });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// q0 is the reference quadrille
let q0, q;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  drawQuadrille(q, { x: mouseX, y: mouseY, outline: 'lime' });
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
The [outline]({{< ref "outline" >}}) parameter is part of the object literal used to customize display options, defining the color of the border drawn around each cell.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, { x, y })`

## Parameters

| Param | Description                                                 |
|-------|-------------------------------------------------------------|
| `x`   | Number: The x-coordinate of the upper-left corner in pixels |
| `y`   | Number: The y-coordinate of the upper-left corner in pixels |