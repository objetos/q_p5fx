---
weight: 5  
draft: false  
title: outlineWeight  
---

Defines the default outline weight (stroke thickness) for drawing the quadrille cells. The default value is `Quadrille.outlineWeight`, which is `2`.

## Example

{{< p5-global-iframe quadrille="true" width="665" height="340" >}}
'use strict';
// Set a common cell length of 40 pixels for both quadrilles
Quadrille.cellLength = 40;
let q1, q2;
let weightSlider;

function setup() {
  createCanvas(640, 315);
  // Quadrille with a fixed outline weight
  q1 = createQuadrille(8, 8);
  // Quadrille with an adjustable outline weight
  q2 = createQuadrille(8, 8);
  // Create a slider to adjust the outline weight for q1
  weightSlider = createSlider(1, 10, 2, 0.5);
  weightSlider.position(10, height - 20);
}

function draw() {
  background('lightblue');
  // Draw q1 with an outline weight controlled by the slider
  drawQuadrille(q1, { outlineWeight: weightSlider.value() });
  // Draw q2 using the default Quadrille.outlineWeight
  drawQuadrille(q2, { x: 330 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// Set a common cell length of 40 pixels for both quadrilles
Quadrille.cellLength = 40;
let q1, q2;
let weightSlider;

function setup() {
  createCanvas(640, 315);
  // Quadrille with a fixed outline weight
  q1 = createQuadrille(8, 8);
  // Quadrille with an adjustable outline weight
  q2 = createQuadrille(8, 8);
  // Create a slider to adjust the outline weight for q1
  weightSlider = createSlider(1, 10, 2, 0.5);
  weightSlider.position(10, height - 20);
}

function draw() {
  background('lightblue');
  // Draw q1 with an outline weight controlled by the slider
  drawQuadrille(q1, { outlineWeight: weightSlider.value() });
  // Draw q2 using the default Quadrille.outlineWeight
  drawQuadrille(q2, { x: 330 });
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**  
In this example, `q1` is drawn with an outline weight controlled by the slider, while `q2` uses the default global `Quadrille.outlineWeight`, which is `2`.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, { outlineWeight })`

## Parameters

| Param         | Description                                                                            |
|---------------|----------------------------------------------------------------------------------------|
| outlineWeight | Number: Specifies the outline weight (stroke thickness). The default is `Quadrille.outlineWeight`, which is `2` |