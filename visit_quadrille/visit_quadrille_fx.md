---
weight: 1
title: visitQuadrille(quadrille, fx)
---

[p5.js](https://p5js.org/) function that visits all cells in the `quadrille`, executing the specified `fx` function on each cell. The function takes `(row, col)` as parameters to define the cell's position.

## Example

The sketch below implements a visit to the upper quadrille, filling its empty cells that have exactly three neighbors, and stores the result in the lower quadrille:

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let source, target;
Quadrille.cellLength = 20;
const w = 600 / Quadrille.cellLength;
const h = 400 / Quadrille.cellLength;
let yellow, blue, red;

function setup() {
  createCanvas(600, 400);
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  source = createQuadrille(w - 2, (h / 2) - 2, 50, yellow);
  source.rand(50, blue);
  target = createQuadrille(w - 2, (h / 2) - 2);
  visitQuadrille(source, (row, col) => {
    if (source.isEmpty(row, col) && source.ring(row, col).order === 3) {
      target.fill(row, col, red);
    }
  });
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
  blue = color('blue');
  red = color('red');
  source = createQuadrille(w - 2, (h / 2) - 2, 50, yellow);
  source.rand(50, blue);
  target = createQuadrille(w - 2, (h / 2) - 2);
  visitQuadrille(source, (row, col) => {
    if (source.isEmpty(row, col) && source.ring(row, col).order === 3) {
      target.fill(row, col, red);
    }
  });
}

function draw() {
  background('coral');
  drawQuadrille(source, { outline: 'white', row: 1, col: 1 });
  drawQuadrille(target, { outline: 'cyan', row: (h / 2) + 1, col: 1 });
}
```
{{< /details >}}

{{< callout type="warning" >}}
**Observation**  
To implement the above sketch, the following quadrille methods are used: [isEmpty()]({{< ref "is_empty" >}}), [ring]({{< ref "ring" >}}), [rand(times, value)]({{< ref "rand_times_value" >}}) and [fill(row, col, value)]({{< ref "fill_row_col_value" >}}).
{{< /callout >}}

## Syntax

> `visitQuadrille(quadrille, fx)`

## Parameters

| parameter | description                                                                                   |
|-----------|-----------------------------------------------------------------------------------------------|
| quadrille | Quadrille: The `quadrille` to be visited                                                      |
| fx        | Function: A function of the form `fx(row, col)` to be executed on all visited cells           |