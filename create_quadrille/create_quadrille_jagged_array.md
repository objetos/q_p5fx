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

function preload() {
  // Load images in preload so that they are ready before setup
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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

{{< details title="code" open=false >}}
```js
let sb; // Image variable
let quadrille;
let yellow, blue, red;

function preload() {
  // Load images in preload so that they are ready before setup
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
{{< /details >}}

{{< callout type="info" >}}  
**Observation about images**  
Images must be loaded in the [preload](https://p5js.org/reference/p5/preload) function using [loadImage](https://p5js.org/reference/p5/loadImage) to ensure they are fully available before [setup](https://p5js.org/reference/p5/setup) or [draw](https://p5js.org/reference/p5/draw) run. This avoids timing issues and ensures smooth rendering.
{{< /callout >}}

## Example 2: Videos, Text, Colors, Numbers, and Emojis

(click to toggle the video playback)  
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let destino; // Video variable
let quadrille;
let yellow, blue, red;

function preload() {
  // Load image and video in preload
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
  destino = createVideo(['/videos/destino.webm']);
  destino.hide(); // Hide video controls
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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

{{< details title="code" open=false >}}
```js
let sb; // Image variable
let destino; // Video variable
let quadrille;
let yellow, blue, red;

function preload() {
  // Load image and video in preload
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
  destino = createVideo(['/videos/destino.webm']);
  destino.hide(); // Hide video controls
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
{{< /details >}}

{{< callout type="info" >}}
**Observations about video**  
1. **Loading the Video:** Videos should be loaded in `preload()` and immediately hidden using the `destino` [hide](https://p5js.org/reference/p5.Element/hide/) method to remove default controls.  
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

## Example 3: WEBGL Mode with Functions, Images, Text, and Colors

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let font; // Custom font
let quadrille;
let yellow, blue, red;

function preload() {
  // Load image and font in preload
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
  font = loadFont('/fonts/noto_sans.ttf');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength, WEBGL);
  textFont(font);
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Quadrille containing cell functions and other content
  quadrille = createQuadrille([
    ['hi', 100, sb, pulse, null, 0],
    [null, yellow, pulse, ':)'],
    [null, blue, pulse, 255, ':p'],
    [null, red, null, 185, ';)', pulse]
  ]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille, { origin: CORNER }); // Render the quadrille
}

function pulse() {
  background('green');
  const radius = map(sin(frameCount * 0.1), -1, 1, 5, Quadrille.cellLength / 2);
  noStroke();
  fill('cyan');
  circle(0, 0, radius);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let sb; // Image variable
let font; // Custom font
let quadrille;
let yellow, blue, red;

function preload() {
  // Load image and font in preload
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
  font = loadFont('/fonts/noto_sans.ttf');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength, WEBGL);
  textFont(font);
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  // Quadrille containing cell functions and other content
  quadrille = createQuadrille([
    ['hi', 100, sb, pulse, null, 0],
    [null, yellow, pulse, ':)'],
    [null, blue, pulse, 255, ':p'],
    [null, red, null, 185, ';)', pulse]
  ]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille, { origin: CORNER }); // Render the quadrille
}

function pulse() {
  background('green');
  const radius = map(sin(frameCount * 0.1), -1, 1, 5, Quadrille.cellLength / 2);
  noStroke();
  fill('cyan');
  circle(0, 0, radius);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observations about [WEBGL](https://p5js.org/reference/p5/WEBGL/) mode and function cells**  
1. **[createCanvas](https://p5js.org/reference/p5/createCanvas/) with `WEBGL` and Function Cells:** Passing `WEBGL` as the third parameter in [createCanvas](https://p5js.org/reference/p5/createCanvas/) enables support for function cells, such as `pulse`.
2. **Function Cells and 3D Geometry:** In `WEBGL` mode, function cells can render 3D geometry using shapes like [`box`](https://p5js.org/reference/p5/box), [`sphere`](https://p5js.org/reference/p5/sphere), and other 3D primitives.  
3. **Font Limitations:** In `WEBGL` mode, fonts must be loaded manually, and emojis are not supported (the only known limitation). 
4. **Origin in WEBGL vs P2D:** In `WEBGL` mode, the origin defaults to the **center** of the canvas, while in `P2D` mode, it defaults to the **top-left corner**. To ensure the quadrille aligns correctly in `WEBGL` mode, the `origin` option is explicitly set to `CORNER` using: `drawQuadrille(quadrille, { origin: CORNER })`.
5. **Origin in Function Cells:** Similarly, within function cells (like `pulse`), the origin is also the **center**. Therefore, `circle(0, 0, radius)` draws a circle centered at the cell’s origin.
{{< /callout >}}

## Example 4: p5.Graphics, Images, Text, Colors, and Emojis

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let pg; // p5.Graphics object
let quadrille;
let yellow, blue, red;

function preload() {
  // Load image in preload
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
  pg.background('green');
  const radius = map(sin(frameCount * 0.1), -1, 1, 5, Quadrille.cellLength / 2);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width / 2, pg.height / 2, radius);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let sb; // Image variable
let pg; // p5.Graphics object
let quadrille;
let yellow, blue, red;

function preload() {
  // Load image in preload
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
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
  pg.background('green');
  const radius = map(sin(frameCount * 0.1), -1, 1, 5, Quadrille.cellLength / 2);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width / 2, pg.height / 2, radius);
}
```
{{< /details >}}

{{< callout type="info" >}}  
**Observations about [p5.Graphics](https://p5js.org/reference/p5/p5.Graphics/) cells**  
1. **Alternative to function cells:** `p5.Graphics` can be used instead of function cells and works in both `P2D` and `WEBGL` modes, but the resulting code is less clean compared to function cells.  
2. **Requires a separate p5.Graphics object:** A `p5.Graphics` object (`pg`) must be created using `createGraphics`, usually with dimensions matching the cell size.  
3. **Origin in P2D mode:** In this example, the origin is the **top-left corner**, so `pg.circle(pg.width / 2, pg.height / 2, radius)` centers the circle within the cell.  
4. **Manual update trigger:** `p5.Graphics` requires an explicit update call, such as from `draw`, which makes it less concise than function cells.  
5. **Performance:** `p5.Graphics` is less efficient than function cells, which are more performant.  
{{< /callout >}}

{{< callout type="warning" >}}
Function cells are the preferred choice in this API's examples while occasionally using `p5.Graphics`.
{{< /callout >}}

## Syntax  

> `createQuadrille(jagged_array)`

## Parameters  

| Parameter    | Description                                                                                         |
|--------------|-----------------------------------------------------------------------------------------------------|
| `jagged_array` | An array containing any combination of valid JavaScript values. Use `null` to represent empty cells |