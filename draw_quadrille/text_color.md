---
weight: 7  
draft: false  
title: textColor  
---

Defines the default text color used for drawing the quadrille cells. The default value is `Quadrille.textColor`, which is `'DodgerBlue'`.

## Example

{{< p5-global-iframe quadrille="true" width="670" height="180" >}}
'use strict';
// Set a common cell length of 40 pixels for both quadrilles
Quadrille.cellLength = 40;
let q1, q2;
let colorPicker;

function setup() {
  createCanvas(650, 160);
  q1 = createQuadrille(8, 'cronopiofabulosaliteratatangente');
  q2 = createQuadrille(8, 'galaxiassoñadorainfinitoarmónico');
  colorPicker = createColorPicker('magenta'); 
  colorPicker.position(10, height - 25);
}

function draw() {
  background('#FFC0CB');
  // Draw q1 using the text color set by the color picker
  drawQuadrille(q1, { textColor: colorPicker.value() });
  // Draw q2 using the default Quadrille.textColor
  drawQuadrille(q2, { x: 330 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// Set a common cell length of 40 pixels for both quadrilles
Quadrille.cellLength = 40;
let q1, q2;
let colorPicker;

function setup() {
  createCanvas(650, 160);
  q1 = createQuadrille(8, 'cronopiofabulosaliteratatangente');
  q2 = createQuadrille(8, 'galaxiassoñadorainfinitoarmónico');
  colorPicker = createColorPicker('magenta'); 
  colorPicker.position(10, height - 25);
}

function draw() {
  background('#FFC0CB');
  // Draw q1 using the text color set by the color picker
  drawQuadrille(q1, { textColor: colorPicker.value() });
  // Draw q2 using the default Quadrille.textColor
  drawQuadrille(q2, { x: 330 });
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**  
In this example, `q1` is drawn with a text color controlled by the color picker, while `q2` uses the default global `Quadrille.textColor`, which is `'DodgerBlue'`.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, { textColor })`

## Parameters

| Param     | Description                                                                            |
|-----------|----------------------------------------------------------------------------------------|
| textColor | String \| [p5.Color](https://p5js.org/reference/#/p5.Color): Specifies the color used for drawing the text. The default is `Quadrille.textColor`, which is `'DodgerBlue'` |