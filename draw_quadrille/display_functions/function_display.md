---
weight: 6
draft: false
title: functionDisplay
---

Static method for drawing cells that are filled with `function` instances.

Pierre

## Example

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
'use strict';

function setup() {
  createCanvas(400, 400, WEBGL);
}

function draw() {
  background('red');
  //translate(-width / 2, -height / 2);
  Quadrille.colorDisplay({graphics: this, origin: CORNER, value: 'cyan', cellLength: width / 2});
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let color;

function setup() {
  createCanvas(165, 165, WEBGL);
  color = createColorPicker('magenta');
}

function draw() {
  background('blue');
  Quadrille.colorDisplay({value: color.value(), cellLength: width});
}
```
{{< /details >}}

## Syntax

> `Quadrille.imageDisplay({graphics, value, [cellLength]})`

## Parameters

| parameter  | description                                                                                 |
|------------|---------------------------------------------------------------------------------------------|
| graphics   | [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): renderer target                    |
| value      | [p5.Color](https://p5js.org/reference/#/p5.Color): cell contents                            |
| cellLength | Number: edge length in pixels default is [Quadrille.cellLength]({{< ref "cell_length" >}}) |
