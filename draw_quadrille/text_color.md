---
weight: 4
draft: false  
title: textColor
---

Defines the default text color used for drawing the quadrille cells. The default value is `Quadrille.textColor`, which is `'DodgerBlue'`.

## Example

{{< p5-global-iframe quadrille="true" width="675" height="355" >}}
'use strict';
// Set a common cell length of 40 pixels for all quadrilles
Quadrille.cellLength = 40;
let q1, q2, q3, q4;
let localPicker, globalPicker;

function setup() {
  createCanvas(650, 330);
  q1 = createQuadrille(8, 'cronopiofabulosaliteratatangente');
  q2 = createQuadrille(8, 'galaxiassoñadorainfinitoarmónico');
  q3 = createQuadrille(8, 'ensueñoscaprichosilencioaventura');
  q4 = createQuadrille(8, 'claridadlecturasmisterioviajeros');
  localPicker = createColorPicker('magenta'); 
  localPicker.position(10, 10);
  // Initialize global picker with the default Quadrille.textColor value
  globalPicker = createColorPicker(Quadrille.textColor); 
  globalPicker.position(340, 10);
  globalPicker.input(() => Quadrille.textColor = globalPicker.value());
}

function draw() {
  background('#FFC0CB');
  // Draw q1 using the text color set by the local color picker
  drawQuadrille(q1, { textColor: localPicker.value() });
  // Draw q2, q3, and q4 using Quadrille.textColor set by the global picker
  drawQuadrille(q2, { x: 330 });
  drawQuadrille(q3, { y: 170 });
  drawQuadrille(q4, { x: 330, y: 170 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// Set a common cell length of 40 pixels for all quadrilles
Quadrille.cellLength = 40;
let q1, q2, q3, q4;
let localPicker, globalPicker;

function setup() {
  createCanvas(650, 330);
  q1 = createQuadrille(8, 'cronopiofabulosaliteratatangente');
  q2 = createQuadrille(8, 'galaxiassoñadorainfinitoarmónico');
  q3 = createQuadrille(8, 'ensueñoscaprichosilencioaventura');
  q4 = createQuadrille(8, 'claridadlecturasmisterioviajeros');
  localPicker = createColorPicker('magenta'); 
  localPicker.position(10, 10);
  // Initialize global picker with the default Quadrille.textColor value
  globalPicker = createColorPicker(Quadrille.textColor); 
  globalPicker.position(340, 10);
  globalPicker.input(() => Quadrille.textColor = globalPicker.value());
}

function draw() {
  background('#FFC0CB');
  // Draw q1 using the text color set by the local color picker
  drawQuadrille(q1, { textColor: localPicker.value() });
  // Draw q2, q3, and q4 using Quadrille.textColor set by the global picker
  drawQuadrille(q2, { x: 330 });
  drawQuadrille(q3, { y: 170 });
  drawQuadrille(q4, { x: 330, y: 170 });
}
```
{{< /details >}}

{{< callout type="info" >}}
- `q1` is drawn with a text color controlled by the local color picker (`localPicker`), initialized to `'magenta'`.  
- `q2`, `q3`, and `q4` use the global `Quadrille.textColor` set by the global color picker (`globalPicker`).
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, { textColor })`

## Parameters

| Param     | Description                                                                            |
|-----------|----------------------------------------------------------------------------------------|
| `textColor` | String \| [p5.Color](https://p5js.org/reference/#/p5.Color): Specifies the color used for drawing the text. The default is `Quadrille.textColor`, which is `'DodgerBlue'` |