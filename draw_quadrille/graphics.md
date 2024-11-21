---
weight: 10
draft: false
title: graphics
---

## Example 1

(click and drag the canvas to move the quadrille graphics)\
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 50;
let quadrille;
let pg;

function setup() {
  createCanvas(600, 400);
  // Create a quadrille and fill it with random emojis
  quadrille = createQuadrille(6, 4).rand(8, '🐉').rand(8, '🦄').fill('🦖');
  // Create a graphics object to render the quadrille
  pg = createGraphics(300, 200);
}

function draw() {
  background('#101010');
  // Draw the quadrille directly on the main canvas
  drawQuadrille(quadrille, { row: 2, col: 3 });
  // Draw the quadrille onto the graphics object
  drawQuadrille(quadrille, { graphics: pg });
  // Render the graphics object dynamically at the mouse position
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
  // Create a quadrille and fill it with random emojis
  quadrille = createQuadrille(6, 4).rand(8, '🐉').rand(8, '🦄').fill('🦖');
  // Create a graphics object to render the quadrille
  pg = createGraphics(300, 200);
}

function draw() {
  background('#101010');
  // Draw the quadrille directly on the main canvas
  drawQuadrille(quadrille, { row: 2, col: 3 });
  // Draw the quadrille onto the graphics object
  drawQuadrille(quadrille, { graphics: pg });
  // Render the graphics object dynamically at the mouse position
  mouseIsPressed && image(pg, mouseX, mouseY);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**  
This example demonstrates how to render a quadrille onto a `p5.Graphics` object and use it as a dynamic image (`image()`) that can be repositioned with the mouse. This allows for layering and independent manipulation of graphical content.
{{< /callout >}}

## Example 2

(click and drag to orbit; dynamic Game of Life pattern rendered as a 3D texture)\
{{< p5-global-iframe quadrille="true" width="625" height="425" >}}
'use strict';
Quadrille.cellLength = 20;
let game, pattern;
let life;
let graphics;

function setup() {
  // Initialize a quadrille for the Game of Life simulation
  game = createQuadrille(20, 20);
  life = color('lime');
  pattern = createQuadrille(3, 16252911n, life);
  game = Quadrille.or(game, pattern, 6, 8);
  // Set up a WEBGL canvas and a graphics object for texture rendering
  createCanvas(game.width * Quadrille.cellLength,
               game.height * Quadrille.cellLength,
               WEBGL);
  graphics = createGraphics(game.width * Quadrille.cellLength,
                            game.height * Quadrille.cellLength, WEBGL);
  update();
}

function draw() {
  background('yellow');
  orbitControl(); // Enable mouse interaction for 3D view
  frameCount % 20 === 0 && update();
  noStroke();
  rotateY(PI);
  sphere(100); // Display a textured sphere
}

function update() {
  const next = game.clone();
  // Implement Game of Life rules
  visitQuadrille(game, (row, col) => {
                       const order = game.ring(row, col).order;
                       game.isFilled(row, col) ?
                       (order < 3 || order > 4) && next.clear(row, col) :
                       order === 3 && next.fill(row, col, life);
                   });
  game = next;
  graphics.background('blue');
  // Render the updated game state onto the graphics object
  drawQuadrille(game, { graphics, outline: 'magenta', origin: CORNER });
  texture(graphics); // Apply the graphics object as a texture
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 20;
let game, pattern;
let life;
let graphics;

function setup() {
  // Initialize a quadrille for the Game of Life simulation
  game = createQuadrille(20, 20);
  life = color('lime');
  pattern = createQuadrille(3, 16252911n, life);
  game = Quadrille.or(game, pattern, 6, 8);
  // Set up a WEBGL canvas and a graphics object for texture rendering
  createCanvas(game.width * Quadrille.cellLength,
               game.height * Quadrille.cellLength,
               WEBGL);
  graphics = createGraphics(game.width * Quadrille.cellLength,
                            game.height * Quadrille.cellLength, WEBGL);
  update();
}

function draw() {
  background('yellow');
  orbitControl(); // Enable mouse interaction for 3D view
  frameCount % 20 === 0 && update();
  noStroke();
  rotateY(PI);
  sphere(100); // Display a textured sphere
}

function update() {
  const next = game.clone();
  // Implement Game of Life rules
  visitQuadrille(game, (row, col) => {
                       const order = game.ring(row, col).order;
                       game.isFilled(row, col) ?
                       (order < 3 || order > 4) && next.clear(row, col) :
                       order === 3 && next.fill(row, col, life);
                   });
  game = next;
  graphics.background('blue');
  // Render the updated game state onto the graphics object
  drawQuadrille(game, { graphics, outline: 'magenta', origin: CORNER });
  texture(graphics); // Apply the graphics object as a texture
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**  
This example illustrates how a quadrille can be rendered as a 3D texture in a WEBGL scene. The Game of Life logic updates the quadrille's state, and the `graphics` object serves as a texture applied to the 3D model (a sphere in this case). The `graphics` parameter decouples the rendering of the quadrille from the main canvas, enabling advanced visualizations.
{{< /callout >}}

## Syntax

> `drawQuadrille(quadrille, { graphics })`

## Parameters

| Param    | Description                                                                                                |
|----------|------------------------------------------------------------------------------------------------------------|
| graphics | [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): Renderer target. Defaults to `this` (main canvas) |