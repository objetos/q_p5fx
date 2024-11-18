---
weight: 1  
draft: false  
title: cellLength  
---

Defines the drawing cell length for quadrilles in pixels. The default is `Quadrille.cellLength`, which is `100`.

## Example

{{< p5-global-iframe quadrille="true" width="665" height="340" >}}
'use strict';
// Set the global cell length to a fixed value of 40 pixels (default is 100)
Quadrille.cellLength = 40;
let q1, q2;
let lengthSlider;

function setup() {
  createCanvas(640, 315);
  // Quadrille with a resizable cell length (controlled by the slider)
  q1 = createQuadrille(8, 8);
  // Quadrille with a fixed cell length of 40 pixels
  q2 = createQuadrille(8, 8);
  // Create a slider to adjust the cell length for q1
  lengthSlider = createSlider(20, 40, 30, 1);
  lengthSlider.position(10, height - 20);
}

function draw() {
  background('#DFFF00');
  // Draw q1 with a cell length controlled by the slider
  drawQuadrille(q1, { cellLength: lengthSlider.value() });
  // Draw q2 using the fixed global Quadrille.cellLength of 40 pixels
  drawQuadrille(q2, { x: 330 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// Set the global cell length to a fixed value of 40 pixels (default is 100)
Quadrille.cellLength = 40;
let q1, q2;
let lengthSlider;

function setup() {
  createCanvas(640, 315);
  // Quadrille with a resizable cell length (controlled by the slider)
  q1 = createQuadrille(8, 8);
  // Quadrille with a fixed cell length of 40 pixels
  q2 = createQuadrille(8, 8);
  // Create a slider to adjust the cell length for q1
  lengthSlider = createSlider(20, 40, 30, 1);
  lengthSlider.position(10, height - 20);
}

function draw() {
  background('#DFFF00');
  // Draw q1 with a cell length controlled by the slider
  drawQuadrille(q1, { cellLength: lengthSlider.value() });
  // Draw q2 using the fixed global Quadrille.cellLength of 40 pixels
  drawQuadrille(q2, { x: 330 });
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**  
In this example, `q1` is drawn with a cell length controlled by the slider, while `q2` uses the fixed global `Quadrille.cellLength` set to `40` pixels.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, { cellLength })`

## Parameters

| Param      | Description                                                                                 |
|------------|---------------------------------------------------------------------------------------------|
| cellLength | Number: Specifies the cell length in pixels. The default is `Quadrille.cellLength`, which is `100` |