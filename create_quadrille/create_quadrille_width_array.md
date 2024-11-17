---
weight: 6
draft: false
title: "createQuadrille(width, array)"
---

Creates a quadrille and fills its cells using the items from the `array`, arranging them across a specified `width` number of columns. The quadrille will have one or more rows depending on the size of the array.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb;
let pg;
let quadrille;

function preload() {
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
  quadrille = createQuadrille(3, ['hi', 100, sb, color('red'), pg]);
}

function draw() {
  background('orange');
  update();
  drawQuadrille(quadrille);
}

function update() {
  pg.background('green');
  let radius = map(mouseX, 0, width, 10, pg.width);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width/2, pg.height/2, radius);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let sb;
let pg;
let quadrille;

function preload() {
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
  quadrille = createQuadrille(3, ['hi', 100, sb, color('red'), pg]);
}

function draw() {
  background('orange');
  update();
  drawQuadrille(quadrille);
}

function update() {
  pg.background('green');
  let radius = map(mouseX, 0, width, 10, pg.width);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width/2, pg.height/2, radius);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**\
The `createQuadrille(width, array)` function allows you to control the number of columns (`width`) while filling the quadrille with the items from the provided `array`.
{{< /callout >}}

## Syntax

> `createQuadrille(width, array)`

## Parameters

| param | description                                                                                                                                        |
|-------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| width | Number: The total number of columns for the quadrille.                                                                                              |
| array | An array containing any combination of [p5.Image](https://p5js.org/reference/#/p5.Image), [p5.Graphics](https://p5js.org/reference/#/p5.Graphics), [p5.Color](https://p5js.org/reference/#/p5.Color), arrays, objects, strings, numbers, or `null` cells. |