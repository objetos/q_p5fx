---
weight: 7
draft: false
title: "createQuadrille(FEN)"
---

Creates a quadrille with the chess board position described by the given [FEN](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation).

## Example

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
'use strict';
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

{{< callout type="info" >}}
**Observation**\
The `createQuadrille(FEN)` function enables the creation of chess board positions based on the given Forsyth–Edwards Notation (FEN). See more about the FEN format [here](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation).
{{< /callout >}}

## Syntax

> `createQuadrille(FEN)`

## Parameters

| param | description                                                                                                                                          |
|-------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| FEN   | String: A valid [Forsyth–Edwards Notation](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation) describing a particular board position.    |