---
bookCollapseSection: true
title: "display functions"
weight: 11
draft: false
---

The display functions define how the quadrille cell data is to be displayed:

1. `tileDisplay`: define the cell contour display.
2. `imageDisplay`: define the cell image display.
3. `stringDisplay`: define the cell string display.
4. `colorDisplay`: define the cell color display.
5. `numberDisplay`: define the cell number display.
6. `arrayDisplay`: define the cell array display.
7. `objectDisplay`: define the cell object display.

{{< callout type="warning" >}}
**Observations**  
1. The `arrayDisplay` and `objectDisplay` methods don't have ([static](https://developer.mozilla.org/en-US/docs/Glossary/Static_method)) defaults.
2. The object literal used to parameterize these functions can have the following properties: `{ quadrille, graphics, outline, outlineWeight, cellLength, textColor, textZoom, value, row, col, width, height }`, where `value` holds the cell contents, `row` and `col` hold the cell position within the `quadrille` and `ẁidth` and `height` are defined as `quadrille.width` and `quadrille.height`, resp. The remaining properties (`outline`, `cellLength`,...) are taken from the `drawQuadrille` method params themselves.
{{< /callout >}}

The following code snippet demonstrates how to display quadrille cells as circles:

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let quadrille;
let circled;
let tileDisplay;// (all) quadrille cell contours
let colorDisplay;// quadrille color cells

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  circled = createCheckbox('circled', true);
  circled.position(10, 10);
  circled.style('color', 'magenta');
  tileDisplay = ({ outline, outlineWeight, cellLength }) => {
    noFill();
    stroke(outline);
    strokeWeight(outlineWeight);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  };
  colorDisplay = ({ value, cellLength }) => {
    noStroke();
    fill(value);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  }
  quadrille = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  let params = {
    x: mouseX,
    y: mouseY,
    tileDisplay: circled.checked() ? tileDisplay : Quadrille.tileDisplay,
    colorDisplay: circled.checked() ? colorDisplay : Quadrille.colorDisplay
  }
  drawQuadrille(quadrille, params);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let quadrille;
let circled;
let tileDisplay;// (all) quadrille cell contours
let colorDisplay;// quadrille color cells

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  circled = createCheckbox('circled', true);
  circled.position(10, 10);
  circled.style('color', 'magenta');
  tileDisplay = ({ outline, outlineWeight, cellLength }) => {
    noFill();
    stroke(outline);
    strokeWeight(outlineWeight);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  };
  colorDisplay = ({ value, cellLength }) => {
    noStroke();
    fill(value);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  }
  quadrille = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  let params = {
    x: mouseX,
    y: mouseY,
    tileDisplay: circled.checked() ? tileDisplay : Quadrille.tileDisplay,
    colorDisplay: circled.checked() ? colorDisplay : Quadrille.colorDisplay
  }
  drawQuadrille(quadrille, params);
}
```
{{< /details >}}

## Syntax

> `drawQuadrille(quadrille, [{[graphics], [x], [y], [col], [row], [cells], [tileDisplay], [imageDisplay], [colorDisplay], [stringDisplay], [numberDisplay], [arrayDisplay], [objectDisplay], [cellLength], [outlineWeight], [outline], [textColor], [textZoom]}])`

## Parameters

| parameter     | description                                                                                               |
|---------------|-----------------------------------------------------------------------------------------------------------|
| tileDisplay   | Function: empty cell drawing custom procedure default is [Quadrille.tileDisplay]({{< ref "tile_display" >}})[^1].  Use `0`, `null` or `undefined` to discard all edges |
| imageDisplay  | Function: image filled cell drawing custom procedure default is [Quadrille.imageDisplay]({{< ref "image_display" >}})    |
| colorDisplay  | Function: color filled cell drawing custom procedure default is [Quadrille.colorDisplay]({{< ref "color_display" >}})    |
| stringDisplay | Function: string filled cell drawing custom procedure default is [Quadrille.stringDisplay]({{< ref "string_display" >}}) |
| numberDisplay | Function: number filled cell drawing custom procedure default is [Quadrille.numberDisplay]({{< ref "number_display" >}}) |
| arrayDisplay  | Function: array filled cell drawing custom procedure                                                      |
| objectDisplay | Function: object filled cell drawing custom procedure                                                     |

[^1]: This function allows to implementing other [regular tilings](https://en.wikipedia.org/wiki/Euclidean_tilings_by_convex_regular_polygons#Regular_tilings) different than the default [square tiling](https://en.wikipedia.org/wiki/Square_tiling).