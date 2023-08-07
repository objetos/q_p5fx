---
weight: 2
draft: false
---

# drawQuadrille

[p5.js](https://p5js.org/) function that draws the quadrille at `(x, y)` screen position on the [`graphics`](https://p5js.org/reference/#/p5.Graphics) (which is the main [`canvas`](https://p5js.org/reference/#/p5/createCanvas) by default), using the display parameter values which are discussed in the following sections.

```js
drawQuadrille(quadrille, [{
  [graphics=this],
  [x],
  [y],
  [col],
  [row],
  [cellLength=Quadrille.CELL_LENGTH],
  [outlineWeight=Quadrille.OUTLINE_WEIGHT],
  [outline=Quadrille.OUTLINE],
  [textColor=Quadrille.TEXT_COLOR],
  [textZoom=Quadrille.TEXT_ZOOM],
  [tileDisplay=Quadrille.TILE],
  [imageDisplay=Quadrille.IMAGE],
  [stringDisplay=Quadrille.STRING],
  [colorDisplay=Quadrille.COLOR],
  [numberDisplay=Quadrille.NUMBER],
  [arrayDisplay],
  [objectDisplay]
}])
```

## Positioning

The quadrille origin (i.e., upper left corner) can be set either with the `x` & `y` or the `row` & `col` drawing params.

### x & y

The `x` and `y` params define the quadrille upper left corner in pixels.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="x_y" width="625" height="425" >}}
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
Observe the use of the `mouseRow` and `mouseCol` [quadrille properties](/docs/Quadrille_API/properties/) used to positioning the `q` quadrille below.
{{< /hint >}}

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="row_col" width="625" height="425" >}}
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

{{< hint warning >}}
**Observation**  
Before going into this section it is good idea to study first the coding train tutorial on arrow functions:
   {{< youtube id="mrYMzpbFz18" title="arrow functions tutorial" >}}
{{< /hint >}}

The display functions define how the quadrille cell data is to be displayed:
1. `tileDisplay`: define the cell contour display.
2. `imageDisplay`: define the cell image display.
3. `stringDisplay`: define the cell string display.
4. `colorDisplay`: define the cell color display.
5. `numberDisplay`: define the cell number display.
6. `arrayDisplay`: define the cell array display.
7. `objectDisplay`: define the cell object display.

{{< hint warning >}}
**Observation**  
The `arrayDisplay` and `objectDisplay` methods don't have ([static](https://developer.mozilla.org/en-US/docs/Glossary/Static_method)) defaults.
{{< /hint >}}

The following code snippet demonstrates how to display quadrille cells as circles:

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="425" >}}
`use strict`;
let quadrille;
let circled;
let tileDisplay;
let colorDisplay;
// imageDisplay, stringDisplay;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  circled = createCheckbox('circled', true);
  circled.position(10, 10);
  circled.style('color', 'magenta');
  // { graphics: graphics, cell: cell, outline: outline, outlineWeight: outlineWeight, cellLength: cellLength, row: i, col: j }
  tileDisplay = ({ outline: outline, outlineWeight: outlineWeight, cellLength: cellLength }) => {
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
// ✨ user provided functions to customize the quadrille display
// the object literal used to parameterize these functions can have the following properties:
// { graphics, cell, outline, outlineWeight, cellLength, row, col }
// cell holds the cell contents
// row and col holds the cell position within the quadrille
// and the remaining properties are taken from the drawQuadrille method call itself
let tileDisplay;// (all) quadrille cell contours
let colorDisplay;// quadrille color cell

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  circled = createCheckbox('circled', true);
  circled.position(10, 10);
  circled.style('color', 'magenta');
  tileDisplay = ({ outline: outline, outlineWeight: outlineWeight, cellLength: cellLength }) => {
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

{{< hint info >}}
**Exercises**     
1. Implement the remaining display functions: `imageDisplay`, `stringDisplay`, `numberDisplay`, `arrayDisplay` and `objectDisplay`.
2. Implement other [regular tilings](https://en.wikipedia.org/wiki/Euclidean_tilings_by_convex_regular_polygons#Regular_tilings) different than the default [square tiling](https://en.wikipedia.org/wiki/Square_tiling).
{{< /hint >}}

## Remaining params

{{< hint info >}}
**Exercise**     
Implement a sketch to test the remaining quadrille drawing params: `cellLength`, `outlineWeight`, `outline`, `textColor` and `textZoom`, some of which are demonstrated within the [boolean operators](/docs/Quadrille_API/boolean_operators/) code snippets.
{{< /hint >}}