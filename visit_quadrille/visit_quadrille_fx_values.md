---
weight: 2
title: visitQuadrille(quadrille, fx, values)
---

[p5.js](https://p5js.org/) function that selectively visits cells in the `quadrille` with specified `values`, executing the given `fx` function on each cell. This function takes `(row, col)` as parameters to define the cell's position.

## Example

The sketch below implements a visit to the upper quadrille, clearing `yellow` and `blue` cells that have more than two neighbors, and stores the result in the lower quadrille:

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let source, target;
Quadrille.cellLength = 20;
const w = 600 / Quadrille.cellLength;
const h = 400 / Quadrille.cellLength;
let yellow, blue, red;

function setup() {
  createCanvas(600, 400);
  yellow = color('yellow');
  red = color('red');
  blue = color('blue');
  source = createQuadrille(w - 2, (h / 2) - 2, 30, yellow);
  source.rand(30, blue).rand(30, red);
  target = source.clone();
  visitQuadrille(source, (row, col) => {
    if (source.ring(row, col).order > 3) {
      target.clear(row, col);
    }
  }, [yellow, blue]);
}

function draw() {
  background('coral');
  drawQuadrille(source, { outline: 'white', row: 1, col: 1 });
  drawQuadrille(target, { outline: 'cyan', row: (h / 2) + 1, col: 1 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let source, target;
Quadrille.cellLength = 20;
const w = 600 / Quadrille.cellLength;
const h = 400 / Quadrille.cellLength;
let yellow, blue, red;

function setup() {
  createCanvas(600, 400);
  yellow = color('yellow');
  red = color('red');
  blue = color('blue');
  source = createQuadrille(w - 2, (h / 2) - 2, 30, yellow);
  source.rand(30, blue).rand(30, red);
  target = source.clone();
  visitQuadrille(source, (row, col) => {
    if (source.ring(row, col).order > 3) {
      target.clear(row, col);
    }
  }, [yellow, blue]);
}

function draw() {
  background('coral');
  drawQuadrille(source, { outline: 'white', row: 1, col: 1 });
  drawQuadrille(target, { outline: 'cyan', row: (h / 2) + 1, col: 1 });
}
```
{{< /details >}}

## Syntax

> `visitQuadrille(quadrille, fx, values)`

## Parameters

| parameter | description                                                                                      |
|-----------|--------------------------------------------------------------------------------------------------|
| quadrille | Quadrille: The `quadrille` to be visited                                                         |
| fx        | Function: A function of the form `fx(row, col)` to be executed on each cell matching `values`    |
| values    | [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): Cells to visit; all cells are visited if this parameter is `undefined` |