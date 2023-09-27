---
weight: 2
draft: false
---

# drawQuadrille

[p5.js](https://p5js.org/) function that draws a `quadrille`.

# Examples

## Positioning

The quadrille origin (i.e., upper left corner) can be set either with the `x` & `y` or the `row` & `col` drawing params.

### x & y

The `x` and `y` params define the quadrille upper left corner in pixels.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="625" height="425" >}}
`use strict`;
// q0 is defined as reference quadrille
let q0, q;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  // an object literal param is used to pass custom drawing properties
  drawQuadrille(q, { x: mouseX, y: mouseY, outline: 'lime' });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// q0 is defined as reference quadrille
let q0, q;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  // an object literal param is used to pass custom drawing properties
  drawQuadrille(q, { x: mouseX, y: mouseY, outline: 'lime' });
}
```
{{< /details >}}

### row & col

The `row` and `col` params define the quadrille upper left corner in rows and cols units.

{{< hint warning >}}
**Observation**  
Observe the `mouseRow` and `mouseCol` [quadrille properties](/docs/Quadrille_API/properties/) calls used to positioning the `q` quadrille below.
{{< /hint >}}

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="625" height="425" >}}
`use strict`;
// q0 is defined as reference quadrille
let q0, q;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  // an object literal param is used to pass custom drawing properties
  drawQuadrille(q, { row: q0.mouseRow, col: q0.mouseCol, outline: 'lime' });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// q0 is defined as reference quadrille
let q0, q;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  q0 = createQuadrille(6, 4);
  q = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(q0);
  // an object literal param is used to pass custom drawing properties
  drawQuadrille(q, { row: q0.mouseRow, col: q0.mouseCol, outline: 'lime' });
}
```
{{< /details >}}

## Display functions

The display functions define how the quadrille cell data is to be displayed:
1. `tileDisplay`: define the cell contour display.
2. `imageDisplay`: define the cell image display.
3. `stringDisplay`: define the cell string display.
4. `colorDisplay`: define the cell color display.
5. `numberDisplay`: define the cell number display.
6. `arrayDisplay`: define the cell array display.
7. `objectDisplay`: define the cell object display.

{{< hint warning >}}
**Observations**  
1. The `arrayDisplay` and `objectDisplay` methods don't have ([static](https://developer.mozilla.org/en-US/docs/Glossary/Static_method)) defaults.
2. The object literal used to parameterize these functions can have the following properties: `{ quadrille, graphics, outline, outlineWeight, cellLength, textColor, textZoom, row, col, cell }`, where `row` and `col` hold the cell position within the quadrille and `cell` holds the cell contents. The remaining properties (`outline`, `cellLength`,...) are taken from the `drawQuadrille` method params themselves.
{{< /hint >}}

The following code snippet demonstrates how to display quadrille cells as circles:

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="625" height="425" >}}
`use strict`;
let quadrille;
let circled;
let tileDisplay;// (all) quadrille cell contours
let colorDisplay;// quadrille color cells

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  circled = createCheckbox('circled', true);
  circled.position(10, 10);
  circled.style('color', 'magenta');
  tileDisplay = ({ 
    outline: outline, outlineWeight: outlineWeight,
    cellLength: cellLength }) => {
    noFill();
    stroke(outline);
    strokeWeight(outlineWeight);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  };
  colorDisplay = ({ cell: cell, cellLength: cellLength }) => {
    noStroke();
    fill(cell);
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
    tileDisplay: circled.checked() ? tileDisplay : Quadrille.TILE,
    colorDisplay: circled.checked() ? colorDisplay : Quadrille.COLOR
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
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  circled = createCheckbox('circled', true);
  circled.position(10, 10);
  circled.style('color', 'magenta');
  tileDisplay = ({ 
    outline: outline, outlineWeight: outlineWeight,
    cellLength: cellLength }) => {
    noFill();
    stroke(outline);
    strokeWeight(outlineWeight);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  };
  colorDisplay = ({ cell: cell, cellLength: cellLength }) => {
    noStroke();
    fill(cell);
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
    tileDisplay: circled.checked() ? tileDisplay : Quadrille.TILE,
    colorDisplay: circled.checked() ? colorDisplay : Quadrille.COLOR
  }
  drawQuadrille(quadrille, params);
}
```
{{< /details >}}

# Syntax

> `drawQuadrille(quadrille, [{[graphics], [x], [y], [col], [row], [cells], [tileDisplay], [imageDisplay], [colorDisplay], [stringDisplay], [numberDisplay], [arrayDisplay], [objectDisplay], [cellLength], [outlineWeight], [outline], [textColor], [textZoom]}])`

# Parameters

| parameter     | description                                                                                               |
|---------------|-----------------------------------------------------------------------------------------------------------|
| quadrille     | Quadrille: `quadrille` to be drawn                                                                        |
| graphics      | [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): renderer target default is `this` (main canvas)  |
| tileDisplay   | Function: empty cell drawing custom procedure default is [Quadrille.TILE]({{< ref "tile" >}})[^1].  Use `0`, `null` or `undefined` to discard all edges |
| imageDisplay  | Function: image filled cell drawing custom procedure default is [Quadrille.IMAGE]({{< ref "image" >}})    |
| colorDisplay  | Function: color filled cell drawing custom procedure default is [Quadrille.COLOR]({{< ref "color" >}})    |
| stringDisplay | Function: string filled cell drawing custom procedure default is [Quadrille.STRING]({{< ref "string" >}}) |
| numberDisplay | Function: number filled cell drawing custom procedure default is [Quadrille.NUMBER]({{< ref "number" >}}) |
| arrayDisplay  | Function: array filled cell drawing custom procedure                                                      |
| objectDisplay | Function: object filled cell drawing custom procedure                                                     |
| x             | Number: upper left quadrille pixel x coordinate default is `0`. Takes higher precedence than `col`        |
| y             | Number: upper left quadrille pixel y coordinate default is `0`. Takes higher precedence than `row`        |
| col           | Number: upper left quadrille col default is `0`.                                                          |
| row           | Number: upper left quadrille row default is `0`.                                                          |
| cells         | [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): cells to be drawn. All cells are drawn if this parameter is `undefined` |
| cellLength    | Number: edge length in pixels default is [Quadrille.CELL_LENGTH]({{< ref "cell_length" >}})               |
| outlineWeight | Number: edge weight default is [Quadrille.OUTLINE_WEIGHT]({{< ref "outline_weight" >}}).                  |
| outline       | [p5.Color](https://p5js.org/reference/#/p5.Color) representation: edge color default is [Quadrille.OUTLINE]({{< ref "outline" >}}) |
| textColor     | [p5.Color](https://p5js.org/reference/#/p5.Color) representation: text color default is [Quadrille.TEXT_COLOR]({{< ref "text_color" >}}) |
| textZoom      | Number:: text zoom level default is [Quadrille.TEXT_ZOOM]({{< ref "text_zoom" >}})                        |

[^1]: This function allows to implementing other [regular tilings](https://en.wikipedia.org/wiki/Euclidean_tilings_by_convex_regular_polygons#Regular_tilings) different than the default [square tiling](https://en.wikipedia.org/wiki/Square_tiling).