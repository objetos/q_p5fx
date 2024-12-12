---
weight: 4
draft: false
title: "createQuadrille(jagged_array)"
---

Creates a quadrille and fills its cells using the items from the [jagged_array](https://en.wikipedia.org/wiki/Jagged_array) as the source. The array can contain any combination of [valid JavaScript values](https://www.w3schools.com/js/js_datatypes.asp), with `null` representing empty cells.

## Example 1: with images, strings (& emojis), colors, numbers cells

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb;
let quadrille;
let yellow, blue, red;

function preload() {
  // loading an image should be done in preload
  // https://p5js.org/reference/#/p5/preload
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  quadrille = createQuadrille([['hi', 100, sb, sb, null, 0],
                               [null, yellow, sb, '🐷'],
                               [null, blue, sb, 255, '🦙'],
                               [null, red, null, 185, '🦜', sb]
                               ]);
}

function draw() {
  // https://htmlcolorcodes.com/
  background('#DAF7A6');
  drawQuadrille(quadrille);
}
{{< /p5-global-iframe >}}

## Example 2:: with videos, strings (& emojis), colors, numbers with video cells

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb;
let destino;
let quadrille;
let yellow, blue, red;

function preload() {
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
  destino = createVideo(['/videos/destino.webm']);
  destino.hide();
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  quadrille = createQuadrille([
    ['hi', 100, sb, sb, null, 0],
    [null, yellow, sb, '🐷'],
    [null, blue, destino, 255, '🦙'],
    [null, red, null, 185, '🦜', sb]
  ]);
}

function draw() {
  background('#DAF7A6');
  drawQuadrille(quadrille);
}

function mouseClicked() {
  // Use the looping property to check the state
  if (destino.looping) {
    destino.pause();
    destino.looping = false; // Update the state
  } else {
    destino.loop();
    destino.looping = true; // Update the state
  }
}
{{< /p5-global-iframe >}}

## Example 3: WEBGL mode with images, strings (but no emojis), colors, numbers and cell functions

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb;
let font;
let quadrille;
let yellow, blue, red;

function preload() {
  // loading an image should be done in preload
  // https://p5js.org/reference/#/p5/preload
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
  font = loadFont('/fonts/noto_sans.ttf');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength, WEBGL);
  textFont(font);
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  quadrille = createQuadrille([['hi', 100, sb, pulse, null, 0],
                               [null, yellow, pulse, ':)'],
                               [null, blue, pulse, 255, ':p'],
                               [null, red, null, 185, ';)', pulse]
                               ]);
}

function draw() {
  // https://htmlcolorcodes.com/
  background('#DAF7A6');
  drawQuadrille(quadrille, { origin: CORNER });
}

function pulse() {
  background('green');
  // Use sine wave to create smooth grow/shrink effect
  const radius = map(sin(frameCount * 0.05), -1, 1, 10, Quadrille.cellLength / 2);
  noStroke();
  fill('cyan');
  circle(0, 0, radius);
}
{{< /p5-global-iframe >}}

## Example 4: : with images, strings (& emojis), colors, and p5.Graphics cells

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
let sb;
let pg;
let quadrille;
let yellow, blue, red;

function preload() {
  // loading an image should be done in preload
  // https://p5js.org/reference/#/p5/preload
  sb = loadImage('/images/simon_bolivar_wedding.jpg');
}

function setup() {
  createCanvas(6 * Quadrille.cellLength, 4 * Quadrille.cellLength);
  yellow = color('yellow');
  blue = color('blue');
  red = color('red');
  pg = createGraphics(Quadrille.cellLength, Quadrille.cellLength);
  quadrille = createQuadrille([['hi', 100, sb, pg, null, 0],
                               [null, yellow, pg, '🐷'],
                               [null, blue, pg, 255, '🦙'],
                               [null, red, null, 185, '🦜', pg]
                               ]);
}

function draw() {
  // https://htmlcolorcodes.com/
  background('#DAF7A6');
  pulse();
  drawQuadrille(quadrille);
}

function pulse() {
  pg.background('green');
  // Use sine wave to create smooth grow/shrink effect
  const radius = map(sin(frameCount * 0.05), -1, 1, 10, pg.width / 2);
  pg.noStroke();
  pg.fill('cyan');
  pg.circle(pg.width / 2, pg.height / 2, radius);
}
{{< /p5-global-iframe >}}

## Syntax

> `createQuadrille(jagged_array)`

## Parameters

| param        | description                                                                                          |
|--------------|------------------------------------------------------------------------------------------------------|
| jagged_array | An array containing any combination of valid JavaScript values, with `null` representing empty cells |