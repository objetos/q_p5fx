---
weight: 2
draft: false
title: colorDisplay
---

Static method for drawing cells that are filled with colors.

## Example

{{< p5-global-iframe quadrille="true" width="190" height="225" >}}
'use strict';
let color;

function setup() {
  createCanvas(165, 165);
  color = createColorPicker('magenta');
}

function draw() {
  background('blue');
  Quadrille.colorDisplay({graphics: this, value: color.value(), cellLength: width});
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let color;

function setup() {
  createCanvas(165, 165);
  color = createColorPicker('magenta');
}

function draw() {
  background('blue');
  Quadrille.colorDisplay({graphics: this, value: color.value(), cellLength: width});
}
```
{{< /details >}}

## Syntax

> `Quadrille.colorDisplay({graphics, value, [cellLength]})`

## Parameters

| parameter  | description                                                                                 |
|------------|---------------------------------------------------------------------------------------------|
| graphics   | [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): renderer target                    |
| value      | [p5.Color](https://p5js.org/reference/#/p5.Color): cell contents                            |
| cellLength | Number: edge length in pixels default is [Quadrille.cellLength]({{< ref "cell_length" >}}) |
