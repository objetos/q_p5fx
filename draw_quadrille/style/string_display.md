---
weight: 15
draft: false
title: stringDisplay
---

Static method for drawing cells that are filled with colors.

Used by [drawQuadrille]({{< ref "draw_quadrille" >}}) and [sample](https://objetos.github.io/p5.quadrille.js/docs/visual_computing/sample/).

## Example

{{< p5-global-iframe quadrille="true" width="205" height="230" >}}
`use strict`;
let string;

function setup() {
  createCanvas(180, 180);
  string = createInput('hola');
}

function draw() {
  background('tomato');
  Quadrille.stringDisplay({ graphics: this, value: string.value(), cellLength: width, textZoom: 0.65 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let string;

function setup() {
  createCanvas(180, 180);
  string = createInput('hola');
}

function draw() {
  background('tomato');
  Quadrille.stringDisplay({ graphics: this, value: string.value(),
                            cellLength: width, textZoom: 0.65 });
}
```
{{< /details >}}

## Syntax

> `Quadrille.stringDisplay({graphics, value, [cellLength], [textColor], [textZoom]})`

## Parameters

| parameter  | description                                                                                 |
|------------|---------------------------------------------------------------------------------------------|
| graphics   | [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): renderer target                    |
| value      | [p5.Color](https://p5js.org/reference/#/p5.Color): cell contents                            |
| cellLength | Number: edge length in pixels default is [Quadrille.cellLength]({{< ref "cell_length" >}}) |
| textColor     | [p5.Color](https://p5js.org/reference/#/p5.Color) representation: text color default is [Quadrille.textColor]({{< ref "text_color" >}}) |
| textZoom      | Number:: text zoom level default is [Quadrille.textZoom]({{< ref "text_zoom" >}})       |
