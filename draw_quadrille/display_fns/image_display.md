---
weight: 5
draft: false
title: imageDisplay
---

Static method for drawing cells that are filled with [p5.Image](https://p5js.org/reference/#/p5.Image) or [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) instances.

## Example

{{< p5-global-iframe quadrille="true" width="190" height="190" >}}
'use strict';
let al;

function preload() {
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  createCanvas(165, 165);
}

function draw() {
  background('blue');
  Quadrille.imageDisplay({ graphics: this, value: al, cellLength: width });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let al;

function preload() {
  al = loadImage('abraham_lincoln.jpg');
}

function setup() {
  createCanvas(165, 165);
}

function draw() {
  background('blue');
  Quadrille.imageDisplay({ graphics: this, value: al, cellLength: width });
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
