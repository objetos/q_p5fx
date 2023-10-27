---
weight: 3
draft: false
---

# visitQuadrille

[p5.js](https://p5js.org/) function that visits `quadrille` cells executing the `fx` function taking `(row, col)` params (which defines the quadrille visited cell position) either on all cells or those defined by the `values` array.

# Examples

## visitQuadrille(quadrille, fx)

The sketch below implements a visit to the upper quadrille to filling its empty cells which have exactly three neighbors and stores the result in the lower quadrille:

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="625" height="425" >}}
`use strict`;
let source, target;
Quadrille.CELL_LENGTH = 20;
const w = 600 / Quadrille.CELL_LENGTH;
const h = 400 / Quadrille.CELL_LENGTH;
// refer to https://htmlcolorcodes.com/
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
Quadrille.CELL_LENGTH = 20;
const w = 600 / Quadrille.CELL_LENGTH;
const h = 400 / Quadrille.CELL_LENGTH;
// refer to https://htmlcolorcodes.com/
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

{{< hint warning >}}
**Observation**  
To implement the above sketch the [isEmpty, ring](/docs/Quadrille_API/main_methods/#read-methods), [rand and fill](/docs/Quadrille_API/main_methods/#write-methods) quadrille methods are used.
{{< /hint >}}

## visitQuadrille(quadrille, fx, values)

The sketch below implements a visit to the upper quadrille to clearing the `yellow` and `blue` cells which have more than two neighbors and stores the result in the lower quadrille:

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" width="625" height="425" >}}
`use strict`;
let source, target;
Quadrille.CELL_LENGTH = 20;
const w = 600 / Quadrille.CELL_LENGTH;
const h = 400 / Quadrille.CELL_LENGTH;
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
Quadrille.CELL_LENGTH = 20;
const w = 600 / Quadrille.CELL_LENGTH;
const h = 400 / Quadrille.CELL_LENGTH;
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

# Syntax

> `createQuadrille(quadrille, fx)`

> `createQuadrille(quadrille, fx, values)`

# Parameters

| parameter     | description                                                                        |
|---------------|------------------------------------------------------------------------------------|
| quadrille     | Quadrille: `quadrille` to be visited                                               |
| fx            | function: function of the form `fx(row, col)` to be executed on all visited cells  |
| values        | [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): cells to be visited. All cells are visited if this parameter is `undefined` |