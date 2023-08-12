---
weight: 1
draft: false
---

# createQuadrille

[p5](https://p5js.org/) [polymorphic](https://en.wikipedia.org/wiki/Ad_hoc_polymorphism) method that creates a [quadrille](https://en.wikipedia.org/wiki/Square_tiling) object whose individual cells may be either `numbers`, `strings`, [p5.Colors](https://p5js.org/reference/#/p5.Color), [p5.Images](https://p5js.org/reference/#/p5.Image) and [p5.Graphics](https://p5js.org/reference/#/p5.Graphics), `arrays` and `object literals`. Drawing a quadrille will be covered separately later on in [another chapter]({{< relref "draw_quadrille" >}}).

{{< hint warning >}}
**Observation**  
Before going into the chapter it is good idea to study first the coding train tutorial on `p5.Graphics`:
   {{< youtube id="TaluaAD9MKA" title="p5.Graphics tutorial" >}}
{{< /hint >}}

# Examples

## createQuadrille(width, height)

Creates an empty quadrille having `width` number of columns and `height` number of rows.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="425" >}}
`use strict`;
// quadrille object declaration
let quadrille;

function setup() {
  // Quadrille.CELL_LENGTH is a constant defining the quadrille
  // cell length default is: 100
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  // quadrille object initialization
  quadrille = createQuadrille(4, 3);
}

function draw() {
  background('violet');
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// quadrille object declaration
let quadrille;

function setup() {
  // Quadrille.CELL_LENGTH is a constant defining the quadrille
  // cell length default is: 100
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  // quadrille object initialization
  quadrille = createQuadrille(4, 3);
}

function draw() {
  background('violet');
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< hint warning >}}
**Observation**  
To run the above sketch you need to include the library in your `html` file, i.e.,
```html
<script src="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.min.js"></script>
```
Have a look the the above p5 editor version of the above example [here](https://editor.p5js.org/nakednous/sketches/fT1twGeXA).
{{< /hint >}}

## createQuadrille(jagged_array)

Creates a quadrille and fills its cells taking the [jagged_array](https://en.wikipedia.org/wiki/Jagged_array) items as source. Note that `null` `array` items represent empty quadrille cells.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="425" >}}
`use strict`;
let al;
let pg;
let quadrille;

function preload() {
  // loading an image should be done in preload
  // https://p5js.org/reference/#/p5/preload
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  // refer to the coding train tutorial linked above
  pg = createGraphics(Quadrille.CELL_LENGTH, Quadrille.CELL_LENGTH);
  quadrille = createQuadrille([['hi', 100, al, pg],
                               [null, color('red'), pg]]);
}

function draw() {
  background('orange');
  update();
  drawQuadrille(quadrille);
}

function update() {
  pg.background('green');
  let radius = map(mouseX, 0, width, 10, pg.width);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width/2, pg.height/2, radius);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let al;
let pg;
let quadrille;

function preload() {
  // loading an image should be done in preload
  // https://p5js.org/reference/#/p5/preload
  al = loadImage('abraham_lincoln.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  // refer to the coding train tutorial linked above
  pg = createGraphics(Quadrille.CELL_LENGTH, Quadrille.CELL_LENGTH);
  quadrille = createQuadrille([['hi', 100,          al, pg],
                               [null, color('red'), pg]]);
}

function draw() {
  background('orange');
  update();
  drawQuadrille(quadrille);
}

function update() {
  pg.background('green');
  let radius = map(mouseX, 0, width, 10, pg.width);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width/2, pg.height/2, radius);
}
```
{{< /details >}}

## createQuadrille(array)

Creates a quadrille and fills its cells taking the `array` items as source. Note that `null` `array` items represent empty quadrille cells.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="425" >}}
`use strict`;
let al;
let pg;
let quadrille;

function preload() {
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  pg = createGraphics(Quadrille.CELL_LENGTH, Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(['hi', 100, al, color('red'), pg]);
}

function draw() {
  background('orange');
  update();
  drawQuadrille(quadrille);
}

function update() {
  pg.background('green');
  let radius = map(mouseX, 0, width, 10, pg.width);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width/2, pg.height/2, radius);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let al;
let pg;
let quadrille;

function preload() {
  al = loadImage('abraham_lincoln.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  pg = createGraphics(Quadrille.CELL_LENGTH, Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(['hi', 100, al, color('red'), pg]);
}

function draw() {
  background('orange');
  update();
  drawQuadrille(quadrille);
}

function update() {
  pg.background('green');
  let radius = map(mouseX, 0, width, 10, pg.width);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width/2, pg.height/2, radius);
}
```
{{< /details >}}

## createQuadrille(width, array)

Creates a quadrille and fills its cells taking the `array` items as source up to `width` number of columns. Observe that (one or) several quadrille rows may be created to include all the `array` items. Note that `null` `array` items represent empty quadrille cells.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="425" >}}
`use strict`;
let al;
let pg;
let quadrille;

function preload() {
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  pg = createGraphics(Quadrille.CELL_LENGTH, Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(3, ['hi', 100, al, color('red'), pg]);
}

function draw() {
  background('orange');
  update();
  drawQuadrille(quadrille);
}

function update() {
  pg.background('green');
  let radius = map(mouseX, 0, width, 10, pg.width);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width/2, pg.height/2, radius);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let al;
let pg;
let quadrille;

function preload() {
  al = loadImage('abraham_lincoln.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  pg = createGraphics(Quadrille.CELL_LENGTH, Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(3, ['hi', 100, al, color('red'), pg]);
}

function draw() {
  background('orange');
  update();
  drawQuadrille(quadrille);
}

function update() {
  pg.background('green');
  let radius = map(mouseX, 0, width, 10, pg.width);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width/2, pg.height/2, radius);
}
```
{{< /details >}}

## createQuadrille(string)

Creates a quadrille and fills its cells taking `string` as source. The resulting number of quadrille `columns` matches that of the [string length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length).

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  quadrille = createQuadrille('hi 👽');
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  quadrille = createQuadrille('hi 👽');
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## createQuadrille(width, string)

Creates a quadrille and fills its cells taking `string` as source. Note that (one or) several quadrille rows may be created to include all the `string` characters.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(2, 'hi 👽');
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(2, 'hi 👽');
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## createQuadrille(width, image, [coherence = false])

Creates a quadrille and fills its cells taking `image` (either a [p5.Image](https://p5js.org/reference/#/p5.Image) or a [p5.Graphics](https://p5js.org/reference/#/p5.Graphics)) as source. The `coherence` boolean param defines whether or not the quadrille filling algorithm should use spatial coherence.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="625" >}}
`use strict`;
let al;
let quadrille;

function preload() {
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  Quadrille.CELL_LENGTH = 25;
  createCanvas(24 * Quadrille.CELL_LENGTH, 24 * Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(24, al);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let al;
let quadrille;

function preload() {
  al = loadImage('abraham_lincoln.jpg');
}

function setup() {
  Quadrille.CELL_LENGTH = 25;
  createCanvas(24 * Quadrille.CELL_LENGTH, 24 * Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(24, al);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## createQuadrille(width, height, order, pattern)

Creates a quadrille and fills its cells using `pattern` (any data type instance but `undefined` or `null`) which is randomly repeated along the quadrille up to `order` number of times.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(4, 3, 7, 150);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  quadrille = createQuadrille(4, 3, 7, 150);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## createQuadrille(width, bitboard, pattern)

Creates a quadrille and fills its cells taking [bitboard](https://en.wikipedia.org/wiki/Bitboard) as source, using `pattern` (any data type instance but `undefined` or `null`) to represent [`1` (or on)](https://en.wikipedia.org/wiki/Bit) bits. For instance the following code snippet draws the [T tetromino](https://en.wikipedia.org/wiki/Tetromino) which may be part of the [tetris](https://en.wikipedia.org/wiki/Tetris) game.

{{< p5-global-iframe lib1="https://cdn.jsdelivr.net/gh/objetos/p5.quadrille.js/p5.quadrille.js" id="number" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  /*
  | 5 | 4 | 3 |
  | 2 | 1 | 0 |
  (0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
  */
  quadrille = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.CELL_LENGTH, 4 * Quadrille.CELL_LENGTH);
  /*
  | 5 | 4 | 3 |
  | 2 | 1 | 0 |
  (0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
  */
  quadrille = createQuadrille(3, 58, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

# Syntax

> `createQuadrille(width, height)`

> `createQuadrille(jagged_array)`

> `createQuadrille(array)`

> `createQuadrille(width, array)`

> `createQuadrille(string)`

> `createQuadrille(width, string)`

> `createQuadrille(width, image, [coherence])`

> `createQuadrille(width, height, order, pattern)`

> `createQuadrille(width, bitboard, pattern)`

# Parameters

| param     | description                                                                                                                                                                   |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| jagged_array | [jagged_array](https://en.wikipedia.org/wiki/Jagged_array): containing any combination of [p5.Image](https://p5js.org/reference/#/p5.Image) \| [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) \| [p5.Color](https://p5js.org/reference/#/p5.Color) \| array \| object \| string \| number \| `null` cells |
| array     | array: containing any combination of [p5.Image](https://p5js.org/reference/#/p5.Image) \| [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) \| [p5.Color](https://p5js.org/reference/#/p5.Color) \| array \| object \| string \| number \| `null` cells |
| string    | String: containing any combination of chars                                                                                                                                   |
| width     | Number: total number of columns                                                                                                                                               |
| height    | Number: total number of rows                                                                                                                                                  |
| image     | [p5.Image](https://p5js.org/reference/#/p5.Image) instance                                                                                                                    |
| coherence | [boolean]: define whether or not to use spatial coherence to convert image default is false                                                                                   |
| bitboard  | Number: [bitboard](https://en.wikipedia.org/wiki/Bitboard) [big-endian](https://en.wikipedia.org/wiki/Endianness) integer representation                                      |
| order     | Number: total number of non-empty cells                                                                                                                                       |
| pattern   | [p5.Image](https://p5js.org/reference/#/p5.Image) \| [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) \| [p5.Color](https://p5js.org/reference/#/p5.Color) \| array \| object \| string \| number \| `null`: empty cells |