---
weight: 5
draft: false  
title: textZoom  
---

Defines the default text zoom level for quadrille cells. The default is `Quadrille.textZoom`, which is `0.89`.

## Example

{{< p5-global-iframe quadrille="true" width="675" height="355" >}}
'use strict';
// Set a common cell length of 40 pixels for all quadrilles
Quadrille.cellLength = 40;
let q1, q2, q3, q4;
let localZoomSlider, globalZoomSlider;

function setup() {
  createCanvas(650, 330);
  q1 = createQuadrille(8, 'cronopiofabulosaliteratatangente');
  q2 = createQuadrille(8, 'galaxiassoñadorainfinitoarmónico');
  q3 = createQuadrille(8, 'ensueñoscaprichosilencioaventura');
  q4 = createQuadrille(8, 'claridadlecturasmisterioviajeros');
  // Local slider to adjust the text zoom level for q1
  localZoomSlider = createSlider(0.1, 0.78, 0.5, 0.01);
  localZoomSlider.position(10, 10);
  // Global slider to set the global Quadrille.textZoom
  globalZoomSlider = createSlider(0.1, 0.78, Quadrille.textZoom, 0.01);
  globalZoomSlider.position(340, 10);
  globalZoomSlider.input(() => Quadrille.textZoom = globalZoomSlider.value());
}

function draw() {
  background('#FFC0CB');
  // Draw q1 with a text zoom level controlled by the local slider
  drawQuadrille(q1, { textZoom: localZoomSlider.value() });
  // Draw q2, q3, and q4 using the global Quadrille.textZoom
  drawQuadrille(q2, { x: 330 });
  drawQuadrille(q3, { y: 170 });
  drawQuadrille(q4, { x: 330, y: 170 });
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
// Set a common cell length of 40 pixels for all quadrilles
Quadrille.cellLength = 40;
let q1, q2, q3, q4;
let localZoomSlider, globalZoomSlider;

function setup() {
  createCanvas(650, 330);
  q1 = createQuadrille(8, 'cronopiofabulosaliteratatangente');
  q2 = createQuadrille(8, 'galaxiassoñadorainfinitoarmónico');
  q3 = createQuadrille(8, 'ensueñoscaprichosilencioaventura');
  q4 = createQuadrille(8, 'claridadlecturasmisterioviajeros');
  // Local slider to adjust the text zoom level for q1
  localZoomSlider = createSlider(0.1, 0.78, 0.5, 0.01);
  localZoomSlider.position(10, 10);
  // Global slider to set the global Quadrille.textZoom
  globalZoomSlider = createSlider(0.1, 0.78, Quadrille.textZoom, 0.01);
  globalZoomSlider.position(340, 10);
  globalZoomSlider.input(() => Quadrille.textZoom = globalZoomSlider.value());
}

function draw() {
  background('#FFC0CB');
  // Draw q1 with a text zoom level controlled by the local slider
  drawQuadrille(q1, { textZoom: localZoomSlider.value() });
  // Draw q2, q3, and q4 using the global Quadrille.textZoom
  drawQuadrille(q2, { x: 330 });
  drawQuadrille(q3, { y: 170 });
  drawQuadrille(q4, { x: 330, y: 170 });
}
```
{{% /details %}}

{{< callout type="info" >}}
- `q1` is drawn with a text zoom level controlled by the local slider (`localZoomSlider`), initialized to `0.5`.  
- `q2`, `q3`, and `q4` use the global `Quadrille.textZoom` set by the global slider (`globalZoomSlider`), which is initially `0.89`.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, { textZoom })`

## Parameters

| Param     | Description                                                                            |
|-----------|----------------------------------------------------------------------------------------|
| `textZoom` | Number: Specifies the text zoom level for drawing the quadrille text. The default is `Quadrille.textZoom`, which is `0.89` |