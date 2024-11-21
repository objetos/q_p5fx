---
weight: 10
draft: false
title: graphics
---

## Example 1

{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 50;
let quadrille;
let pg;

function setup() {
  createCanvas(600, 400);
  quadrille = createQuadrille(6, 4).rand(8, '🐉').rand(8, '🦄').fill('🦖');
  pg = createGraphics(300, 200)
}

function draw() {
  background('#101010');
  drawQuadrille(quadrille, { row: 2, col: 3 });
  drawQuadrille(quadrille, { graphics: pg });
  mouseIsPressed && image(pg, mouseX, mouseY);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 50;
let quadrille;
let pg;

function setup() {
  createCanvas(600, 400);
  quadrille = createQuadrille(6, 4).rand(8, '🐉').rand(8, '🦄').fill('🦖');
  pg = createGraphics(300, 200)
}

function draw() {
  background('#101010');
  drawQuadrille(quadrille, { row: 2, col: 3 });
  drawQuadrille(quadrille, { graphics: pg });
  mouseIsPressed && image(pg, mouseX, mouseY);
}
```
{{< /details >}}

## Example 2

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
'use strict';
Quadrille.cellLength = 20;
let game, pattern;
let life;
let graphics;

function setup() {
  game = createQuadrille(20, 20);
  life = color('lime');
  pattern = createQuadrille(3, 16252911n, life);
  game = Quadrille.or(game, pattern, 6, 8);
  createCanvas(game.width  * Quadrille.cellLength,
               game.height * Quadrille.cellLength,
               WEBGL);
  graphics = createGraphics(game.width  * Quadrille.cellLength,
                            game.height * Quadrille.cellLength, WEBGL);
  update();
}

function draw() {
  background('yellow');
  orbitControl();
  frameCount % 20 === 0 && update();
  noStroke();
  rotateY(PI)
  sphere(100);
}

function update() {
  const next = game.clone();
  visitQuadrille(game, (row, col) => {
                       const order = game.ring(row, col).order
                       game.isFilled(row, col) ?
                       (order < 3 || order > 4) && next.clear(row, col) :
                       order === 3 && next.fill(row, col, life) });
  game = next;
  graphics.background('blue');
  drawQuadrille(game, { graphics, outline: 'magenta', origin: CORNER });
  texture(graphics);
}
{{< /p5-global-iframe >}}


{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 20;
let game, pattern;
let life;
let graphics;

function setup() {
  game = createQuadrille(20, 20);
  life = color('lime');
  pattern = createQuadrille(3, 16252911n, life);
  game = Quadrille.or(game, pattern, 6, 8);
  createCanvas(game.width  * Quadrille.cellLength,
               game.height * Quadrille.cellLength,
               WEBGL);
  graphics = createGraphics(game.width  * Quadrille.cellLength,
                            game.height * Quadrille.cellLength, WEBGL);
  update();
}

function draw() {
  background('yellow');
  orbitControl();
  frameCount % 20 === 0 && update();
  noStroke();
  rotateY(PI)
  sphere(100);
}

function update() {
  const next = game.clone();
  visitQuadrille(game, (row, col) => {
                       const order = game.ring(row, col).order
                       game.isFilled(row, col) ?
                       (order < 3 || order > 4) && next.clear(row, col) :
                       order === 3 && next.fill(row, col, life) });
  game = next;
  graphics.background('blue');
  drawQuadrille(game, { graphics, outline: 'magenta', origin: CORNER });
  texture(graphics);
}
```
{{< /details >}}

## Syntax

> `drawQuadrille(quadrille, { graphics })`

## Parameters

| Param   | Description                                                                                               |
|----------|----------------------------------------------------------------------------------------------------------|
| graphics | [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): renderer target default is `this` (main canvas) |