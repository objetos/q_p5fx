---
weight: 5
draft: false
title: "createQuadrille(array)"
---

The `createQuadrille` function creates a **quadrille** and fills its cells using items from the `array` as the source. The array can contain any combination of [valid JavaScript values](https://www.w3schools.com/js/js_datatypes.asp), with `null` representing empty cells.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="125" >}}
'use strict';
let sb; // Image variable
let quadrille;

function preload() {
  // Load images in preload so that they are ready before setup
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, Quadrille.cellLength);
  // Define the quadrille with diverse content
  quadrille = createQuadrille(['hi', 100, null, sb, '🦜', color('red')]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille); // Render the quadrille
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let sb; // Image variable
let quadrille;

function preload() {
  // Load images in preload so that they are ready before setup
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, Quadrille.cellLength);
  // Define the quadrille with diverse content
  quadrille = createQuadrille(['hi', 100, null, sb, '🦜', color('red')]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille); // Render the quadrille
}
```
{{< /details >}}

{{< callout type="info" >}}
The `createQuadrille(array)` function lets you populate a quadrille with any valid JavaScript values, such as images, colors, and strings, provided in an `array`; for handling these values, see [createQuadrille(jagged_array)]({{< relref "create_quadrille_jagged_array" >}}).
{{< /callout >}}

## Syntax

> `createQuadrille(array)`

## Parameters

| param | description                                                                                                                                        |
|-------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `array` | An array containing any combination of valid JavaScript values. Use `null` to represent empty cells |