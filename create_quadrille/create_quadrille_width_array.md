---
weight: 6  
draft: false  
title: "createQuadrille(width, array)"  
---

The `createQuadrille(width, array)` function creates a **quadrille** with a specified number of columns (`width`) and fills its cells using items from the provided `array`. The items are arranged sequentially across the specified columns, creating one or more rows as needed. The array can contain any combination of [valid JavaScript values](https://www.w3schools.com/js/js_datatypes.asp), with `null` representing empty cells.

## Example

{{< p5-global-iframe quadrille="true" width="325" height="225" >}}
'use strict';
let sb; // Image variable
let quadrille;

function preload() {
  // Load images in preload so that they are ready before setup
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(3 * Quadrille.cellLength, 2 * Quadrille.cellLength);
  // Define the quadrille with diverse content
  quadrille = createQuadrille(3, ['hi', 100, null, sb, '🦜', color('red')]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille); // Render the quadrille
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let sb; // Image variable
let quadrille;

function preload() {
  // Load images in preload so that they are ready before setup
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(3 * Quadrille.cellLength, 2 * Quadrille.cellLength);
  // Define the quadrille with diverse content
  quadrille = createQuadrille(3, ['hi', 100, null, sb, '🦜', color('red')]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille); // Render the quadrille
}
```
{{% /details %}}

{{< callout type="info" >}}  
The `createQuadrille(width, array)` function lets you specify the number of columns (`width`) while filling the quadrille with items from the provided `array`. Items are arranged sequentially into rows, and any `null` values represent empty cells. For handling the values, refer to [createQuadrille(jagged_array)]({{< relref "create_quadrille_jagged_array" >}}).  
{{< /callout >}}

## Syntax  

> `createQuadrille(width, array)`  

## Parameters  

| Param | Description                                                                                                                      |  
|-----------|--------------------------------------------------------------------------------------------------------------------------------------|  
| `width`   | Number: The total number of columns for the quadrille                                                                               |  
| `array`   | An array containing any combination of valid JavaScript values. Use `null` to represent empty cells |  