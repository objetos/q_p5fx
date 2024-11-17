---
weight: 12
draft: false
title: numberDisplay
---

Static method for drawing cells that are filled with numbers. [Implemented](https://github.com/objetos/p5.quadrille.js/blob/main/p5.quadrille.js#L1086) in terms of [Quadrille.colorDisplay]({{< ref "color_display" >}}) as: `Quadrille.colorDisplay({ graphics: graphics, cell: graphics.color(graphics.constrain(cell, 0, 255)), cellLength: cellLength })`.

Used by [drawQuadrille]({{< ref "draw_quadrille" >}}) and [sample](https://objetos.github.io/p5.quadrille.js/docs/visual_computing/sample/).

## Example

{{< p5-global-iframe quadrille="true" width="190" height="220" >}}
'use strict';
let number;

function setup() {
  createCanvas(165, 165);
  number = createSlider(0, 255, 125, 1);
}

function draw() {
  background('blue');
  Quadrille.numberDisplay( { graphics: this, value: number.value(), cellLength: width } );
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let number;

function setup() {
  createCanvas(165, 165);
  number = createSlider(0, 255, 125, 1);
}

function draw() {
  background('blue');
  Quadrille.numberDisplay({graphics: this, value: number.value(), cellLength: width});
}
```
{{< /details >}}

## Syntax

> `Quadrille.numberDisplay({graphics, value, [cellLength]})`

## Parameters

| parameter  | description                                                                                 |
|------------|---------------------------------------------------------------------------------------------|
| graphics   | [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): renderer target                    |
| value      | Number: cell contents                                                                       |
| cellLength | Number: edge length in pixels default is [Quadrille.cellLength]({{< ref "cell_length" >}}) |
