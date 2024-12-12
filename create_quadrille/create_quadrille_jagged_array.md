---
weight: 4  
draft: false  
title: "createQuadrille(jagged_array)"  
---

The `createQuadrille` function creates a **quadrille** and fills its cells using items from a [jagged_array](https://en.wikipedia.org/wiki/Jagged_array). The array can contain any combination of [valid JavaScript values](https://www.w3schools.com/js/js_datatypes.asp), with `null` representing empty cells.

## Example 1: Images, Text, Colors, Numbers, and Emojis  

This example creates a quadrille using a mix of images, numbers, colors, text (including emojis), and empty cells (`null`).  

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let quadrille;
let yellow, blue, red;

function preload() {
  // Load an image in preload for proper rendering
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
  background('#DAF7A6'); // Light green background
  drawQuadrille(quadrille); // Render the quadrille
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let sb; // Image variable
let quadrille;
let yellow, blue, red;

function preload() {
  // Load an image in preload for proper rendering
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
  background('#DAF7A6'); // Light green background
  drawQuadrille(quadrille); // Render the quadrille
}
```
{{< /details >}}

## Example 2: Videos, Text, Colors, Numbers, and Emojis  

This example demonstrates how to use a video along with other content types in the quadrille. Clicking the mouse toggles the video playback.  

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
  if (destino.looping) {
    destino.pause();
    destino.looping = false;
  } else {
    destino.loop();
    destino.looping = true;
  }
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
  if (destino.looping) {
    destino.pause();
    destino.looping = false;
  } else {
    destino.loop();
    destino.looping = true;
  }
}
```
{{< /details >}}

## Example 3: WEBGL Mode with Functions, Images, Text, and Colors  

This example uses **WEBGL mode** and includes a mix of images, colors, and cell functions. The `pulse` function animates a circular effect inside a quadrille cell.  

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let font; // Custom font
let quadrille;
let yellow, blue, red;

function preload() {
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
  font = loadFont('/fonts/noto_sans.ttf'); // Load a custom font
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
  background('#DAF7A6'); // Light green background
  drawQuadrille(quadrille, { origin: CORNER }); // Render the quadrille
}

function pulse() {
  background('green'); // Cell-specific animation
  const radius = map(sin(frameCount * 0.05), -1, 1, 10, Quadrille.cellLength / 2);
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
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
  font = loadFont('/fonts/noto_sans.ttf'); // Load a custom font
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
  background('#DAF7A6'); // Light green background
  drawQuadrille(quadrille, { origin: CORNER }); // Render the quadrille
}

function pulse() {
  background('green'); // Cell-specific animation
  const radius = map(sin(frameCount * 0.05), -1, 1, 10, Quadrille.cellLength / 2);
  noStroke();
  fill('cyan');
  circle(0, 0, radius);
}let sb; // Image variable
let font; // Custom font
let quadrille;
let yellow, blue, red;

function preload() {
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
  font = loadFont('/fonts/noto_sans.ttf'); // Load a custom font
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
  background('#DAF7A6'); // Light green background
  drawQuadrille(quadrille, { origin: CORNER }); // Render the quadrille
}

function pulse() {
  background('green'); // Cell-specific animation
  const radius = map(sin(frameCount * 0.05), -1, 1, 10, Quadrille.cellLength / 2);
  noStroke();
  fill('cyan');
  circle(0, 0, radius);
}
```
{{< /details >}}

## Example 4: p5.Graphics, Images, Text, Colors, and Emojis  

This example demonstrates using **p5.Graphics** as a quadrille cell type. A smooth pulse animation is drawn within a `p5.Graphics` object.  

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb; // Image variable
let pg; // p5.Graphics object
let quadrille;
let yellow, blue, red;

function preload() {
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
  background('#DAF7A6'); // Light green background
  pulse(); // Update the p5.Graphics animation
  drawQuadrille(quadrille); // Render the quadrille
}

function pulse() {
  pg.background('green'); // Draw smooth pulse animation
  const radius = map(sin(frameCount * 0.05), -1, 1, 10, pg.width / 2);
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
  background('#DAF7A6'); // Light green background
  pulse(); // Update the p5.Graphics animation
  drawQuadrille(quadrille); // Render the quadrille
}

function pulse() {
  pg.background('green'); // Draw smooth pulse animation
  const radius = map(sin(frameCount * 0.05), -1, 1, 10, pg.width / 2);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width / 2, pg.height / 2, radius);
}
```
{{< /details >}}

## Syntax  

> `createQuadrille(jagged_array)`

## Parameters  

| Parameter    | Description                                                                                         |
|--------------|-----------------------------------------------------------------------------------------------------|
| jagged_array | An array containing any combination of valid JavaScript values. Use `null` to represent empty cells |