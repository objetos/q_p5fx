---
weight: 1  
draft: false  
title: cellLength  
---

Defines the drawing cell length for quadrilles in pixels. The default is `Quadrille.cellLength`, which is `100`.

## Example

{{< p5-global-iframe quadrille="true" width="665" height="340" >}}
Quadrille.cellLength = 30; // Initial value for the resizable quadrille
let q1, q2;
let lengthSlider;

function setup() {
  createCanvas(640, 315);
  q1 = createQuadrille(8, 8); // Fixed-size quadrille
  q2 = createQuadrille(8, 8); // Resizable quadrille
  lengthSlider = createSlider(20, 40, Quadrille.cellLength, 1);
  lengthSlider.position(10, height - 20);
  lengthSlider.input(() => Quadrille.cellLength = lengthSlider.value());
}

function draw() {
  background('#DFFF00');
  drawQuadrille(q1, { cellLength: 40 });
  drawQuadrille(q2, { x: 330 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 30; // Initial value for the resizable quadrille
let q1, q2;
let lengthSlider;

function setup() {
  createCanvas(640, 315);
  q1 = createQuadrille(8, 8); // Fixed-size quadrille
  q2 = createQuadrille(8, 8); // Resizable quadrille
  lengthSlider = createSlider(20, 40, Quadrille.cellLength, 1);
  lengthSlider.position(10, height - 20);
  lengthSlider.input(() => Quadrille.cellLength = lengthSlider.value());
}

function draw() {
  background('#DFFF00');
  drawQuadrille(q1, { cellLength: 40 });
  drawQuadrille(q2, { x: 330 });
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**  
In this example, `q1` is drawn with a fixed cell length of `40` pixels, while `q2` uses the global `Quadrille.cellLength`, which can be adjusted using the slider.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, { cellLength })`

## Parameters

| Param      | Description                                                                                 |
|------------|---------------------------------------------------------------------------------------------|
| cellLength | Number: Specifies the cell length in pixels. The default is `Quadrille.cellLength`, which is `100` |