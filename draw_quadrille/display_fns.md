---
weight: 12
draft: false  
title: display functions  
---

Display functions determine how quadrille cells are visually rendered based on their values. To disable a specific display function, assign it a value of `0`, `null`, or `undefined`.

| Display Function  | Value Type | Default                                                                                                              |
|-------------------|------------|----------------------------------------------------------------------------------------------------------------------|
| `tileDisplay`     | All cells  | `Quadrille.tileDisplay`: Draws cell contours as square tiles                                                         |
| `stringDisplay`   | String     | `Quadrille.stringDisplay`: Displays strings in cells                                                                 |
| `numberDisplay`   | Number     | `Quadrille.numberDisplay`: Renders numbers in cells as grayscale colors, clamped to the range [0..255] |
| `colorDisplay`    | Color      | `Quadrille.colorDisplay`: Fills cells with specified [p5.Colors](https://p5js.org/reference/#/p5.Color)              |
| `imageDisplay`    | Image      | `Quadrille.imageDisplay`: Draws images in cells                                                                      |
| `functionDisplay` | Function   | `Quadrille.functionDisplay`: Executes a function to draw the cell (available only in WEBGL)                          |
| `arrayDisplay`    | Array      | No static default. It must be explicitly defined if used                                                             |
| `objectDisplay`   | Object     | No static default. It must be explicitly defined if used                                                             |

The object literal used to parameterize these functions can include the following properties: `{` `quadrille`, [cellLength]({{< relref "cell_length" >}}), [outline]({{< relref "outline" >}}), [outlineWeight]({{< relref "outline_weight" >}}), [textColor]({{< relref "text_color" >}}), [textZoom]({{< relref "text_zoom" >}}), [textFont]({{< relref "text_font" >}}), [graphics]({{< relref "graphics" >}}), [origin]({{< relref "origin" >}}), `options`, `value`, `row`, `col`, `width`, `height` `}`. Here, `options` allows passing a custom object to the display function, `value` contains the cell contents, `row` and `col` represent the cell's position in the `quadrille`, and `width` and `height` refer to `quadrille.width` and `quadrille.height`, respectively.

## Example

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let quadrille;
let circled;
let customTile; // Custom tile display for all quadrille cell contours
let customColor; // Custom display for quadrille color cells

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  circled = createCheckbox('circled', true)
    .position(10, 10)
    .style('color', 'magenta');
  customTile = ({ outline, outlineWeight, cellLength }) => {
    noFill();
    stroke(outline);
    strokeWeight(outlineWeight);
    ellipseMode(CORNER);
    circle(0, 0, cellLength);
  };
  customColor = ({ value, cellLength }) => {
    noStroke();
    fill(value);
    ellipseMode(CORNER);
    circle(0, 0, cellLength);
  };
  quadrille = createQuadrille(3, 58n, color('blue'));
}

function draw() {
  background('orange');
  let params = {
    x: mouseX,
    y: mouseY,
    tileDisplay: circled.checked() ? customTile : Quadrille.tileDisplay,
    colorDisplay: circled.checked() ? customColor : Quadrille.colorDisplay
  };
  drawQuadrille(quadrille, params);
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let quadrille;
let circled;
let customTile; // Custom tile display for all quadrille cell contours
let customColor; // Custom display for quadrille color cells

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  circled = createCheckbox('circled', true)
    .position(10, 10)
    .style('color', 'magenta');
  customTile = ({ outline, outlineWeight, cellLength }) => {
    noFill();
    stroke(outline);
    strokeWeight(outlineWeight);
    ellipseMode(CORNER);
    circle(0, 0, cellLength);
  };
  customColor = ({ value, cellLength }) => {
    noStroke();
    fill(value);
    ellipseMode(CORNER);
    circle(0, 0, cellLength);
  };
  quadrille = createQuadrille(3, 58n, color('blue'));
}

function draw() {
  background('orange');
  let params = {
    x: mouseX,
    y: mouseY,
    tileDisplay: circled.checked() ? customTile : Quadrille.tileDisplay,
    colorDisplay: circled.checked() ? customColor : Quadrille.colorDisplay
  };
  drawQuadrille(quadrille, params);
}
```
{{% /details %}}

{{< callout type="info" >}}
This example overrides the default square tiling by supplying JavaScript [arrow functions](https://www.w3schools.com/js/js_arrow_function.asp) to `tileDisplay` and `colorDisplay`, causing each quadrille cell to render as a circle.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, {tileDisplay, stringDisplay, numberDisplay, colorDisplay, imageDisplay, functionDisplay, arrayDisplay, objectDisplay})`

## Parameters

| Param       | Description                                                                                           |
|-----------------|-------------------------------------------------------------------------------------------------------|
| `tileDisplay`[^1] | Function: Renders cell contours. Default is `Quadrille.tileDisplay`                                   |
| `stringDisplay`   | Function: Renders strings in cells. Default is `Quadrille.stringDisplay`                              |
| `numberDisplay`   | Function: Renders numbers in cells. Default is `Quadrille.numberDisplay`                              |
| `colorDisplay`    | Function: Renders colors in cells. Default is `Quadrille.colorDisplay`                                |
| `imageDisplay`    | Function: Renders images in cells. Default is `Quadrille.imageDisplay`                                |
| `functionDisplay` | Function: Renders functions in cells, available only in WEBGL. Default is `Quadrille.functionDisplay` |
| `arrayDisplay`    | Function: Renders cells filled with arrays. No static default provided                                |
| `objectDisplay`   | Function: Renders cells filled with objects. No static default provided                               |

[^1]: The `tileDisplay` function enables the implementation of [regular tilings](https://en.wikipedia.org/wiki/Euclidean_tilings_by_convex_regular_polygons#Regular_tilings) other than the default [square tiling](https://en.wikipedia.org/wiki/Square_tiling).