---
bookCollapseSection: true
title: "display functions"
weight: 13
draft: false
---

Display functions define how quadrille cells are rendered based on their values. Use `0`, `null`, or `undefined` to skip a specific display function.

| Display Function  | Value Type | Default                                                                                     |
|-------------------|------------|---------------------------------------------------------------------------------------------|
| `tileDisplay`     | All cells  | [Quadrille.tileDisplay]({{< ref "tile_display" >}}): Draws cell contours as square tiles    |
| `stringDisplay`   | String     | [Quadrille.stringDisplay]({{< ref "string_display" >}}): Displays strings in cells          |
| `numberDisplay`   | Number     | [Quadrille.numberDisplay]({{< ref "number_display" >}}): Displays numbers in cells, where numbers represent grayscale colors in the range [0..255] |
| `colorDisplay`    | Color      | [Quadrille.colorDisplay]({{< ref "color_display" >}}): Fills cells with specified [p5.Colors](https://p5js.org/reference/#/p5.Color)    |
| `imageDisplay`    | Image      | [Quadrille.imageDisplay]({{< ref "image_display" >}}): Draws images in cells                |
| `functionDisplay` | Function   | [Quadrille.functionDisplay]({{< ref "function_display" >}}): Executes a function to draw the cell (available only in WEBGL) |
| `arrayDisplay`    | Array      | No static default                                                                           |
| `objectDisplay`   | Object     | No static default                                                                           |

{{< callout type="info" >}}
**Observations**  
1. The `arrayDisplay` and `objectDisplay` methods do not have static defaults. They must be explicitly defined if used.  
2. The object literal used to parameterize these functions can include the following properties: `{ quadrille, cellLength, outline, outlineWeight, textColor, textZoom, textFont, graphics, origin, options, value, row, col, width, height }`. Here, `options` allows passing a custom object to the display function, `value` contains the cell contents, `row` and `col` represent the cell's position in the `quadrille`, and `width` and `height` refer to `quadrille.width` and `quadrille.height`, respectively.
{{< /callout >}}

The following example demonstrates customizing `tileDisplay` and `colorDisplay` functions to render quadrille cells as circles:

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let quadrille;
let circled;
let customTile; // Custom tile display for all quadrille cell contours
let customColor; // Custom display for quadrille color cells

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  circled = createCheckbox('circled', true);
  circled.position(10, 10);
  circled.style('color', 'magenta');
  customTile = ({ outline, outlineWeight, cellLength }) => {
    noFill();
    stroke(outline);
    strokeWeight(outlineWeight);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  };
  customColor = ({ value, cellLength }) => {
    noStroke();
    fill(value);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  };
  quadrille = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  let params = {
    x: mouseX,
    y: mouseY,
    tileDisplay: circled.checked() ? customTile : Quadrille.tileDisplay,
    colorDisplay: circled.checked() ? customColor : Quadrille.colorDisplay,
  };
  drawQuadrille(quadrille, params);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let quadrille;
let circled;
let customTile; // Custom tile display for all quadrille cell contours
let customColor; // Custom display for quadrille color cells

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  circled = createCheckbox('circled', true);
  circled.position(10, 10);
  circled.style('color', 'magenta');
  customTile = ({ outline, outlineWeight, cellLength }) => {
    noFill();
    stroke(outline);
    strokeWeight(outlineWeight);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  };
  customColor = ({ value, cellLength }) => {
    noStroke();
    fill(value);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  };
  quadrille = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  let params = {
    x: mouseX,
    y: mouseY,
    tileDisplay: circled.checked() ? customTile : Quadrille.tileDisplay,
    colorDisplay: circled.checked() ? customColor : Quadrille.colorDisplay,
  };
  drawQuadrille(quadrille, params);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observations**  
* This example customizes `tileDisplay` and `colorDisplay` to render quadrille cells as circular shapes, overriding the default square tiling.  
* By toggling the checkbox, the rendering can switch between the custom circular shapes and the default square tiles.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, {tileDisplay, stringDisplay, numberDisplay, colorDisplay, imageDisplay, functionDisplay, arrayDisplay, objectDisplay})`

## Parameters

| Parameter         | Description                                                                                               |
|-------------------|-----------------------------------------------------------------------------------------------------------|
| tileDisplay       | Function: Draws cell contours. Default is [Quadrille.tileDisplay]({{< ref "tile_display" >}}). Use `0`, `null`, or `undefined` to discard edges |
| stringDisplay     | Function: Customizes string rendering in cells. Default is [Quadrille.stringDisplay]({{< ref "string_display" >}}) |
| numberDisplay     | Function: Customizes number rendering in cells. Default is [Quadrille.numberDisplay]({{< ref "number_display" >}}) |
| colorDisplay      | Function: Customizes color rendering in cells. Default is [Quadrille.colorDisplay]({{< ref "color_display" >}}) |
| imageDisplay      | Function: Customizes image rendering in cells. Default is [Quadrille.imageDisplay]({{< ref "image_display" >}}) |
| functionDisplay   | Function: Customizes function-based rendering in cells. Default is [Quadrille.functionDisplay]({{< ref "function_display" >}}) |
| arrayDisplay      | Function: Customizes rendering for array-filled cells. No static default                                 |
| objectDisplay     | Function: Customizes rendering for object-filled cells. No static default                                |

[^1]: The `tileDisplay` parameter enables the implementation of [regular tilings](https://en.wikipedia.org/wiki/Euclidean_tilings_by_convex_regular_polygons#Regular_tilings) other than the default [square tiling](https://en.wikipedia.org/wiki/Square_tiling).