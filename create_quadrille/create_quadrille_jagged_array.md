---
weight: 4  
draft: false  
title: "createQuadrille(jagged_array)"  
---

The `createQuadrille` function creates a **quadrille** and fills its cells using items from a [jagged_array](https://en.wikipedia.org/wiki/Jagged_array). The array can contain any combination of [valid JavaScript values](https://www.w3schools.com/js/js_datatypes.asp), with `null` representing empty cells.

## Example 1: Images, Text, Colors, Numbers, and Emojis

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // Load image
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Define the quadrille with diverse content
  quadrille = createQuadrille([
    ['hi', 100, sb, sb, null, 0],
    [null, yellow, sb, '🐷'],
    [null, blue, sb, 255, '🦙'],
    [null, red, null, 185, '🦜', sb]
  ]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille); // Render the quadrille
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let sb; // Image variable
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // Load image
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Define the quadrille with diverse content
  quadrille = createQuadrille([
    ['hi', 100, sb, sb, null, 0],
    [null, yellow, sb, '🐷'],
    [null, blue, sb, 255, '🦙'],
    [null, red, null, 185, '🦜', sb]
  ]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille); // Render the quadrille
}
```
{{% /details %}}

{{< callout type="info" >}}  
**Observation about images**  
Images are loaded in the `async` [setup](https://p5js.org/reference/p5/setup) function using `await` with [loadImage](https://p5js.org/reference/p5/loadImage) to ensure they are fully available before being used.
{{< /callout >}}

## Example 2: Videos, Text, Colors, Numbers, and Emojis

(click to toggle the video playback)  
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let destino; // Video variable
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // Load image and video
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  destino = await createVideo(['/videos/destino.webm']);
  destino.hide(); // Hide video controls
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Quadrille containing a video, image, text, and colors
  quadrille = createQuadrille([
    ['hi', 100, sb, sb, null, 0],
    [null, yellow, sb, '🐷'],
    [null, blue, destino, 255, '🦙'],
    [null, red, null, 185, '🦜', sb]
  ]);
}

function draw() {
  background('#DAF7A6'); // Light green background
  drawQuadrille(quadrille); // Render the quadrille
}

function mouseClicked() {
  // Toggle video playback on mouse click
  destino.looping ? destino.pause() : destino.loop();
  destino.looping = !destino.looping;
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let sb; // Image variable
let destino; // Video variable
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // Load image and video
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  destino = await createVideo(['/videos/destino.webm']);
  destino.hide(); // Hide video controls
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Quadrille containing a video, image, text, and colors
  quadrille = createQuadrille([
    ['hi', 100, sb, sb, null, 0],
    [null, yellow, sb, '🐷'],
    [null, blue, destino, 255, '🦙'],
    [null, red, null, 185, '🦜', sb]
  ]);
}

function draw() {
  background('#DAF7A6'); // Light green background
  drawQuadrille(quadrille); // Render the quadrille
}

function mouseClicked() {
  // Toggle video playback on mouse click
  destino.looping ? destino.pause() : destino.loop();
  destino.looping = !destino.looping;
}
```
{{% /details %}}

{{< callout type="info" >}}
**Observations about video**  
1. **Loading the Video:** Videos are loaded in the `async` `setup()` function with `await` and immediately hidden using the `destino` [hide](https://p5js.org/reference/p5.Element/hide/) method to remove default controls.  
2. **Interactive Playback Toggle:** This code toggles the video playback when the mouse is clicked:  
   ```javascript
   destino.looping ? destino.pause() : destino.loop();
   destino.looping = !destino.looping;
   ```  
   The [ternary operator](https://www.w3schools.com/js/js_comparisons.asp#ternary) (`condition ? exprIfTrue : exprIfFalse`) is shorthand for `if/else`. Equivalent code:  
   ```javascript
   if (destino.looping) destino.pause();
   else destino.loop();
   ```  
3. **`destino.looping` custom [property](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics):** Initially, `destino.looping` is `undefined` (a [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) value). The line `destino.looping = !destino.looping;` flips its value to `true` on the first click, and subsequently toggles it between `true` and `false`.  
{{< /callout >}}

## Example 3: Functions, Images, Text, Colors and Emojis

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // Load image and font
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Quadrille containing cell functions and other content
  quadrille = createQuadrille([
    ['hi', 100, sb, pulse, null, 0],
    [null, yellow, pulse, '🐷'],
    [null, blue, pulse, 255, '🦙'],
    [null, red, null, 185, '🦜', sb]
  ]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille);
}

function pulse() {
  push();
  const center = Quadrille.cellLength / 2;
  const radius = map(sin(frameCount * 0.1), -1, 1, 5, center);
  noStroke();
  fill('cyan');
  circle(center, center, radius);
  pop();
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let sb; // Image variable
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // Load image and font
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Quadrille containing cell functions and other content
  quadrille = createQuadrille([
    ['hi', 100, sb, pulse, null, 0],
    [null, yellow, pulse, '🐷'],
    [null, blue, pulse, 255, '🦙'],
    [null, red, null, 185, '🦜', sb]
  ]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille);
}

function pulse() {
  push();
  const center = Quadrille.cellLength / 2;
  const radius = map(sin(frameCount * 0.1), -1, 1, 5, center);
  noStroke();
  fill('cyan');
  circle(center, center, radius);
  pop();
}
```
{{% /details %}}

{{< callout type="info" >}}
**Observations about [P2D](https://beta.p5js.org/reference/p5/p2d/) mode and function cells**  
1. **Canvas Mode and Function Cells:** Using `P2D` mode—either by omitting the third argument to `createCanvas()` or explicitly setting it—supports 2D function-based cells like `pulse`.
2. **Origin in the Canvas:** In `P2D` mode, the canvas origin defaults to the **top-left corner**. To position the entire quadrille with its top-left corner at the center of the canvas, use `drawQuadrille(quadrille, { origin: CENTER })`.
3. **Origin in Function Cells:** Likewise, within each function cell (such as `pulse`), the coordinate origin is also the top-left corner of the cell. To draw shapes centered within the cell (like `circle(center, center, radius)`), define `center = Quadrille.cellLength / 2`. Alternatively, pass `options: { origin: CENTER }` to `drawQuadrille()` to shift the coordinate system to the cell center.
{{< /callout >}}

## Example 4: WEBGL Mode with Functions, Images, Text, and Colors

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';

let sb; // Image variable
let font; // Custom font
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength, WEBGL);
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  font = await loadFont('/fonts/noto_sans.ttf');
  textFont(font);
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  quadrille = createQuadrille([
    ['hi', 100, sb, ringTorus, null, 0],
    [null, yellow, ringTorus, ':)'],
    [null, blue, ringTorus, 255, ':p'],
    [null, red, null, 185, ';)', sb]
  ]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille, { origin: CORNER });
}

function ringTorus() {
  push();
  ambientLight(60);
  directionalLight(255, 255, 255, 0.25, 0.25, -1);
  rotateX(frameCount * 0.03);
  rotateY(frameCount * 0.03);
  colorMode(HSB);
  fill((frameCount * 2) % 360, 255, 255);
  noStroke();
  torus(Quadrille.cellLength / 3);
  pop();
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let sb; // Image variable
let font; // Custom font
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength, WEBGL);
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  font = await loadFont('/fonts/noto_sans.ttf');
  textFont(font);
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  quadrille = createQuadrille([
    ['hi', 100, sb, ringTorus, null, 0],
    [null, yellow, ringTorus, ':)'],
    [null, blue, ringTorus, 255, ':p'],
    [null, red, null, 185, ';)', sb]
  ]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille, { origin: CORNER });
}

function ringTorus() {
  push();
  ambientLight(60);
  directionalLight(255, 255, 255, 0.25, 0.25, -1);
  rotateX(frameCount * 0.03);
  rotateY(frameCount * 0.03);
  colorMode(HSB);
  fill((frameCount * 2) % 360, 255, 255);
  noStroke();
  torus(Quadrille.cellLength / 3);
  pop();
}
```
{{% /details %}}

{{< callout type="info" >}}
**Observations about [WEBGL](https://beta.p5js.org/reference/p5/WEBGL/) mode and function cells**  
1. **3D Function Cells:** Using `WEBGL` mode as the third argument to `createCanvas()` enables 3D function-based cells like `ringTorus`, which can render geometry using primitives such as [`box`](https://p5js.org/reference/p5/box), [`sphere`](https://p5js.org/reference/p5/sphere), and [`torus`](https://p5js.org/reference/p5/torus).
2. **Font Limitations:** In `WEBGL` mode, fonts must be loaded manually, and emojis are not supported (the only known limitation).
3. **Origin in the Canvas:** In `WEBGL` mode, the canvas origin defaults to the **center**. To align the top-left of the quadrille with the canvas, use `drawQuadrille(quadrille, { origin: CORNER })`.
4. **Origin in Function Cells:** Likewise, within each function cell (such as `ringTorus`), the coordinate origin is also the center of the cell. To draw from the top-left corner instead, pass `options: { origin: CORNER }` to `drawQuadrille()`.
{{< /callout >}}

<!-- {{< callout type="warning" >}}
The **`WEBGL` mode** in **`p5.js`** has a **higher carbon footprint** due to its reliance on **GPU acceleration**, which consumes more energy. For applications that do not require 3D rendering, consider using **`PGraphics`** with **`P2D` mode** as a more **energy-efficient** and **sustainable** alternative.
{{< /callout >}} -->

## Example 5: p5.Graphics, Images, Text, Colors, and Emojis

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let pg; // p5.Graphics object
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // Load image
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Create a p5.Graphics object for custom drawing
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
  quadrille = createQuadrille([
    ['hi', 100, sb, pg, null, 0],
    [null, yellow, pg, '🐷'],
    [null, blue, pg, 255, '🦙'],
    [null, red, null, 185, '🦜', pg]
  ]);
}

function draw() {
  background('#DAF7A6');
  pulse(); // Update the p5.Graphics animation
  drawQuadrille(quadrille); // Render the quadrille
}

function pulse() {
  pg.background('green'); // p5.Graphics background should explicitly be set
  const radius = map(sin(frameCount * 0.1), -1, 1, 5, Quadrille.cellLength / 2);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width / 2, pg.height / 2, radius);
}
{{< /p5-global-iframe >}}

{{% details title="code" open=true %}}
```js
let sb; // Image variable
let pg; // p5.Graphics object
let quadrille;
let yellow, blue, red;

async function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  // Load image
  sb = await loadImage('/images/simon_bolivar_wedding.jpg');
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Create a p5.Graphics object for custom drawing
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
  quadrille = createQuadrille([
    ['hi', 100, sb, pg, null, 0],
    [null, yellow, pg, '🐷'],
    [null, blue, pg, 255, '🦙'],
    [null, red, null, 185, '🦜', pg]
  ]);
}

function draw() {
  background('#DAF7A6');
  pulse(); // Update the p5.Graphics animation
  drawQuadrille(quadrille); // Render the quadrille
}

function pulse() {
  pg.background('green'); // p5.Graphics background should explicitly be set
  const radius = map(sin(frameCount * 0.1), -1, 1, 5, Quadrille.cellLength / 2);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width / 2, pg.height / 2, radius);
}
```
{{% /details %}}

{{< callout type="info" >}}  
**Observations about [p5.Graphics](https://p5js.org/reference/p5/p5.Graphics/) cells**  
1. **Alternative to function cells:** `p5.Graphics` can be used instead of function cells and works in both `P2D` and `WEBGL` modes, but the resulting code is less clean compared to function cells.  
2. **Requires a separate p5.Graphics object:** A `p5.Graphics` object (`pg`) must be created using `createGraphics`, usually with dimensions matching the cell size.  
3. **Origin in P2D mode:** In this example, the `origin` is the **top-left corner**, so `pg.circle(pg.width / 2, pg.height / 2, radius)` centers the circle within the cell.  
4. **Manual update trigger:** `p5.Graphics` requires an explicit update call, such as from `draw`, which makes it less concise than function cells.  
5. **Performance:** `p5.Graphics` is less efficient than function cells, which are more performant.  
{{< /callout >}}

{{< callout type="warning" >}}
Function cells are the preferred choice in this API's examples while occasionally using `p5.Graphics`.
{{< /callout >}}

## Syntax  

> `createQuadrille(jagged_array)`

## Parameters  

| Param      | Description                                                                                         |
|----------------|-----------------------------------------------------------------------------------------------------|
| `jagged_array` | An array containing any combination of valid JavaScript values. Use `null` to represent empty cells |
