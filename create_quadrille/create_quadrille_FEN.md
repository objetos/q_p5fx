---
weight: 7  
draft: false  
title: "createQuadrille(FEN)"  
---

Creates a quadrille with the chess board position described by the given [FEN](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation).

## Example 1

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
'use strict';
Quadrille.cellLength = 50;
Quadrille.tileDisplay = 0;
Quadrille.textColor = 'black';
const COLS = 8, ROWS = 8;
let board, fen;

function setup() {
  createCanvas(COLS * Quadrille.cellLength, ROWS * Quadrille.cellLength);
  board = createQuadrille();
  fen = createQuadrille('rnbqkbnr/pp1ppppp/8/2p5/4P3/5N2/PPPP1PPP/RNBQKB1R');
}

function draw() {
  drawQuadrille(board);
  drawQuadrille(fen);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 50;
Quadrille.tileDisplay = 0;
Quadrille.textColor = 'black';
const COLS = 8, ROWS = 8;
let board, fen;

function setup() {
  createCanvas(COLS * Quadrille.cellLength, ROWS * Quadrille.cellLength);
  board = createQuadrille();
  fen = createQuadrille('rnbqkbnr/pp1ppppp/8/2p5/4P3/5N2/PPPP1PPP/RNBQKB1R');
}

function draw() {
  drawQuadrille(board);
  drawQuadrille(fen);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Observation**  
`createQuadrille(FEN)` creates a chess board based on the given FEN notation. See more about FEN [here](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation).
{{< /callout >}}

## Example 2: Custom Chess Symbols with Chess.com Colors

{{< p5-global-iframe quadrille="true" width="425" height="425" >}}
'use strict';
Quadrille.cellLength = 50;
Quadrille.tileDisplay = 0;
Quadrille.textColor = 'blue';
// Set Chess.com board colors
Quadrille.lightSquare = '#EBECCF'; // Light square color
Quadrille.darkSquare = '#769555';  // Dark square color
// Set custom chess symbols with emojis
Quadrille.setChessSymbols({
  K: '👑', Q: '💎', R: '🏰', B: '🦅', N: '🐴', P: '🍪',
  k: '🤴', q: '👸', r: '🏯', b: '🦉', n: '🦄', p: '🍩'
});
const FEN = 'rnbqkbnr/pp1ppppp/8/2p5/4P3/5N2/PPPP1PPP/RNBQKB1R';
let board, fenQuadrille;

function setup() {
  createCanvas(8 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  board = createQuadrille(); // Background layer with Chess.com colors
  fenQuadrille = createQuadrille(FEN); // Foreground layer with custom symbols
}

function draw() {
  drawQuadrille(board);
  drawQuadrille(fenQuadrille);
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
Quadrille.cellLength = 50;
Quadrille.tileDisplay = 0;
Quadrille.textColor = 'blue';
// Set Chess.com board colors
Quadrille.lightSquare = '#EBECCF'; // Light square color
Quadrille.darkSquare = '#769555';  // Dark square color
// Set custom chess symbols with emojis
Quadrille.setChessSymbols({
  K: '👑', Q: '💎', R: '🏰', B: '🦅', N: '🐴', P: '🍪',
  k: '🤴', q: '👸', r: '🏯', b: '🦉', n: '🦄', p: '🍩'
});
const FEN = 'rnbqkbnr/pp1ppppp/8/2p5/4P3/5N2/PPPP1PPP/RNBQKB1R';
let board, fenQuadrille;

function setup() {
  createCanvas(8 * Quadrille.cellLength, 8 * Quadrille.cellLength);
  board = createQuadrille(); // Background layer with Chess.com colors
  fenQuadrille = createQuadrille(FEN); // Foreground layer with custom symbols
}

function draw() {
  drawQuadrille(board);
  drawQuadrille(fenQuadrille);
}
```
{{< /details >}}

{{< callout type="info" >}}
**Custom Symbols and Colors**\
This example uses Chess.com colors for the board and custom emoji symbols for the chess pieces. The `setChessSymbols()` function updates both `Quadrille.chessSymbols` and `Quadrille.chessKeys`, enabling reverse lookup of piece symbols.
{{< /callout >}}

{{< callout type="info" >}}
**Default Chess Symbols and Keys**\
If no custom symbols are set, the following default values are used:

```js
// Default chess symbols
static chessSymbols = {
  K: '♔', Q: '♕', R: '♖', B: '♗', N: '♘', P: '♙',
  k: '♚', q: '♛', r: '♜', b: '♝', n: '♞', p: '♟'
};

// Default chess keys (reverse lookup)
static chessKeys = {
  '♔': 'K', '♕': 'Q', '♖': 'R', '♗': 'B', '♘': 'N', '♙': 'P',
  '♚': 'k', '♛': 'q', '♜': 'r', '♝': 'b', '♞': 'n', '♟': 'p'
};
```
{{< /callout >}}

## Syntax

> `createQuadrille(FEN)`

## Parameters

| Param | Description                                                                                                                             |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------|
| FEN   | String: A valid [Forsyth–Edwards Notation](https://en.wikipedia.org/wiki/Forsyth%E2%80%93Edwards_Notation) describing a board position |