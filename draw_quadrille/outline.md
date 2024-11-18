---
weight: 4  
draft: false  
title: outline  
---

Defines the default outline color used for drawing the quadrille cells. The default value is `Quadrille.outline`, which is `'OrangeRed'`.

## Example

{{< p5-global-iframe quadrille="true" width="665" height="340" >}}
'use strict';
// Set a common cell length of 40 pixels for both quadrilles
Quadrille.cellLength = 40;
// Set the global outline color (initially 'OrangeRed', changed to 'cyan' here)
Quadrille.outline = 'cyan';
let q1, q2;
let colorPicker;

function setup() {
  createCanvas(640, 315);
  // Quadrille with an outline color controlled by the color picker
  q1 = createQuadrille(8, 8);
  // Quadrille using the global outline color
  q2 = createQuadrille(8, 8);
  // Initialize the color picker with 'red'
  colorPicker = createColorPicker('red');
  colorPicker.position(10, height - 25);
}

function draw() {
  background('#FFC0CB');
  // Draw q1 with the outline color set by the color picker
  drawQuadrille(q1, { outline: colorPicker.value() });
  // Draw q2 using the current global Quadrille.outline color ('cyan')
  drawQuadrille(q2, { x: 330 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// Set a common cell length of 40 pixels for both quadrilles
Quadrille.cellLength = 40;
// Set the global outline color (initially 'OrangeRed', changed to 'cyan' here)
Quadrille.outline = 'cyan';
let q1, q2;
let colorPicker;

function setup() {
  createCanvas(640, 315);
  // Quadrille with an outline color controlled by the color picker
  q1 = createQuadrille(8, 8);
  // Quadrille using the global outline color
  q2 = createQuadrille(8, 8);
  // Initialize the color picker with 'red'
  colorPicker = createColorPicker('red');
  colorPicker.position(10, height - 25);
}

function draw() {
  background('#FFC0CB');
  // Draw q1 with the outline color set by the color picker
  drawQuadrille(q1, { outline: colorPicker.value() });
  // Draw q2 using the current global Quadrille.outline color ('cyan')
  drawQuadrille(q2, { x: 330 });
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**  
In this example, `q1` is drawn with an outline color controlled by the color picker, while `q2` uses the global `Quadrille.outline` color, which has been set to `'cyan'`.
{{< /callout >}}

## Syntax

> `Quadrille.outline`

## Parameters

| Param    | Description                                                                      |
|----------|----------------------------------------------------------------------------------|
| outline  | String \| [p5.Color](https://p5js.org/reference/#/p5.Color): The color used for drawing the quadrille outline. Default is `Quadrille.outline`, which is `'OrangeRed'` |