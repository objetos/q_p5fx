---
weight: 1
draft: false
---

# createQuadrille

[p5](https://p5js.org/) [polymorphic](https://en.wikipedia.org/wiki/Ad_hoc_polymorphism) method that creates a [quadrille](https://en.wikipedia.org/wiki/Square_tiling) object whose individual cells may be filled either with `numbers`, `strings`, [p5.Colors](https://p5js.org/reference/#/p5.Color), [p5.Images](https://p5js.org/reference/#/p5.Image) and [p5.Graphics](https://p5js.org/reference/#/p5.Graphics), `arrays`, `objects` and `null` which defined empty cells. Drawing a quadrille will be covered separately later on in [another chapter]({{< relref "draw_quadrille" >}}).

{{< hint warning >}}
**Observation**\
Before delving into this function's details, consider reviewing the Coding Train tutorial on `p5.Graphics` first:
   {{< youtube id="TaluaAD9MKA" title="p5.Graphics tutorial" >}}
{{< /hint >}}

# Examples

## createQuadrille()

Creates an 8x8 quadrille with a chessboard pattern.

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
`use strict`;
// Global style vars
// Quadrille cell length default is: 100, we change it to 50
Quadrille.cellLength = 50;
// Disable the tile display algorithm
Quadrille.tileDisplay = 0;
// quadrille object declaration
let quadrille;

function setup() {
  createCanvas(8 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  // quadrille object initialization
  quadrille = createQuadrille();
}

function draw() {
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
// Global style vars
// Quadrille cell length default is: 100, we change it to 50
Quadrille.cellLength = 50;
// Disable the tile display algorithm
Quadrille.tileDisplay = 0;
// quadrille object declaration
let quadrille;

function setup() {
  createCanvas(8 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  // quadrille object initialization
  quadrille = createQuadrille();
}

function draw() {
  // to display the quadrille a call to drawQuadrille is needed
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< hint info >}}
**Observation**\
Observe that `createQuadrille()` is equivalent to `createQuadrille(8, 8).fill()`. See [createQuadrille(width, height)]({{< ref "create_quadrille/#createquadrillewidth-height" >}}) and [fill()]({{< ref "fill" >}}).
{{< /hint >}}

## createQuadrille(width, height)

Creates an empty quadrille having `width` number of columns and `height` number of rows.

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
// quadrille object declaration
let quadrille;

function setup() {
  // Quadrille.cellLength is a constant defining the quadrille
  // cell length default is: 100
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
  // Quadrille.cellLength is a constant defining the quadrille
  // cell length default is: 100
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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

Creates a quadrille and fills its cells taking the [jagged_array](https://en.wikipedia.org/wiki/Jagged_array) items as source.

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
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
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // refer to the coding train tutorial linked above
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
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
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // refer to the coding train tutorial linked above
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
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

Creates a quadrille and fills its cells taking the `array` items as source.

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let al;
let pg;
let quadrille;

function preload() {
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
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
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
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

Creates a quadrille and fills its cells taking the `array` items as source up to `width` number of columns. Observe that (one or) several quadrille rows may be created to include all the `array` items.

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let al;
let pg;
let quadrille;

function preload() {
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
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
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
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

## createQuadrille(FEN)

Creates a quadrille with the chess board position described by the given [FEN](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation).

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
`use strict`;
Quadrille.cellLength = 50;
Quadrille.tileDisplay = 0;
Quadrille.textColor = 'black';
const COLS = 8, ROWS = 8;
// two quadrille layers
let board, fen;

function setup() {
  createCanvas(COLS * Quadrille.cellLength, ROWS * Quadrille.cellLength);
  board = createQuadrille();
  fen = createQuadrille('rnbqkbnr/pp1ppppp/8/2p5/4P3/5N2/PPPP1PPP/RNBQKB1R');
}

function draw() {
  // background quadrille layer
  drawQuadrille(board);
  // foreground quadrille layer drawn on top
  drawQuadrille(fen);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 50;
Quadrille.tileDisplay = 0;
Quadrille.textColor = 'black';
const COLS = 8, ROWS = 8;
// two quadrille layers
let board, fen;

function setup() {
  createCanvas(COLS * Quadrille.cellLength, ROWS * Quadrille.cellLength);
  board = createQuadrille();
  fen = createQuadrille('rnbqkbnr/pp1ppppp/8/2p5/4P3/5N2/PPPP1PPP/RNBQKB1R');
}

function draw() {
  // background quadrille layer
  drawQuadrille(board);
  // foreground quadrille layer drawn on top
  drawQuadrille(fen);
}
```
{{< /details >}}

## createQuadrille(string)

Creates a quadrille and fills its cells taking `string` as source. The resulting number of quadrille `columns` matches that of the [string length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length).

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(2, 'hi 👽');
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## createQuadrille(width, image)

Converts `image` (either a [p5.Image](https://p5js.org/reference/#/p5.Image) or a [p5.Graphics](https://p5js.org/reference/#/p5.Graphics)) into a quadrille.

{{< p5-global-iframe quadrille="true" width="625" height="625" >}}
`use strict`;
let al;
let quadrille;

function preload() {
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
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
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
  quadrille = createQuadrille(24, al);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## createQuadrille(width, image, coherence)

Converts `image` (either a [p5.Image](https://p5js.org/reference/#/p5.Image) or a [p5.Graphics](https://p5js.org/reference/#/p5.Graphics)) into a _pixelated_ quadrille. The `coherence` boolean param defines whether or not the quadrille filling algorithm should use spatial coherence.

{{< p5-global-iframe quadrille="true" width="625" height="625" >}}
`use strict`;
let al;
let quadrille;

function preload() {
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
  quadrille = createQuadrille(24, al, false);
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
  Quadrille.cellLength = 25;
  createCanvas(24 * Quadrille.cellLength, 24 * Quadrille.cellLength);
  quadrille = createQuadrille(24, al, false);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## createQuadrille(width, height, order, value)

Creates a quadrille and fills its cells using `value` (any data type instance but `undefined`) which is randomly repeated along the quadrille up to `order` number of times.

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  quadrille = createQuadrille(4, 3, 7, 150);
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

## createQuadrille(width, bigint, value)

Converts a [bigint](https://www.w3schools.com/js/js_bigint.asp) into a quadrille pattern, filling [`1` (or on)](https://en.wikipedia.org/wiki/Bit) bits with the specified value. For instance the following code snippet draws the [T tetromino](https://en.wikipedia.org/wiki/Tetromino) which may be part of the [tetris](https://en.wikipedia.org/wiki/Tetris) game.

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
`use strict`;
let quadrille;

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  /*
  | 5 | 4 | 3 |
  | 2 | 1 | 0 |
  (0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
  */
  quadrille = createQuadrille(3, 58n, color('blue'));
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
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  /*
  | 5 | 4 | 3 |
  | 2 | 1 | 0 |
  (0)2⁰ + (1)2¹ + (0)2² + (1)2³ + (1)2⁴ + (1)2⁵ = 58
  */
  quadrille = createQuadrille(3, 58n, color('blue'));
}

function draw() {
  background('orange');
  drawQuadrille(quadrille);
}
```
{{< /details >}}

{{< hint info >}}
**Observation**\
Observe that a [bigint](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt) may represent a [bitboard](https://en.wikipedia.org/wiki/Bitboard).
{{< /hint >}}

# Syntax

> `createQuadrille()`

> `createQuadrille(width, height)`

> `createQuadrille(jagged_array)`

> `createQuadrille(array)`

> `createQuadrille(width, array)`

> `createQuadrille(FEN)`

> `createQuadrille(string)`

> `createQuadrille(width, string)`

> `createQuadrille(width, image, [coherence])`

> `createQuadrille(width, height, order, value)`

> `createQuadrille(width, bigint, value)`

# Parameters

| param     | description                                                                                                                                                                   |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| jagged_array | [jagged_array](https://en.wikipedia.org/wiki/Jagged_array): containing any combination of [p5.Image](https://p5js.org/reference/#/p5.Image) \| [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) \| [p5.Color](https://p5js.org/reference/#/p5.Color) \| array \| object \| string \| number \| `null` cells |
| array     | array: containing any combination of [p5.Image](https://p5js.org/reference/#/p5.Image) \| [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) \| [p5.Color](https://p5js.org/reference/#/p5.Color) \| array \| object \| string \| number \| `null` cells |
| FEN       | String: [FEN](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation) describing a particular board position of a chess game                                          |
| string    | String: containing any combination of chars                                                                                                                                   |
| width     | Number: total number of columns                                                                                                                                               |
| height    | Number: total number of rows                                                                                                                                                  |
| image     | [p5.Image](https://p5js.org/reference/#/p5.Image) instance                                                                                                                    |
| coherence | Boolean: define whether or not to use spatial coherence to convert image default is false                                                                                     |
| bigint    | BigInt (or Number): integer representation using [big-endian](https://en.wikipedia.org/wiki/Endianness) byte order |
| order     | Number: total number of non-empty cells                                                                                                                                       |
| value     | [p5.Image](https://p5js.org/reference/#/p5.Image) \| [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) \| [p5.Color](https://p5js.org/reference/#/p5.Color) \| array \| object \| string \| number \| `null`: empty cells |