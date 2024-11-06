---
bookCollapseSection: true
title: "visitQuadrille(args)"
weight: 2
draft: false
---

this chapter introduces how to iterate over `quadrille` cells to execute a `fx` function on each cell. the function just takes 

TODO: arrow functions are introduced here in this chapter.

## Method 1

```js
for (row = 0; row < quadrille.height; row++) {
  for (col = 0; col < quadrille.width; col++) {
    fx(row, col);
  }
}
```

## Method 2 

since a quadrille is an [iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol) object the same results can also be obtained with a [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of) loop:

```js
for (cell of quadrille) {
  // cell is an object literal having value, row and col properties
  fx(cell.row, cell.col);
}
```

## Method 3

the one that cares

[p5.js](https://p5js.org/) function that visits `quadrille` cells executing the `fx` function taking `(row, col)` params (which defines the quadrille visited cell position) either on all cells or those defined by the `values` array. in this chapter visitQuadrille is introduced so the above loops can be simply:

```js
visitQuadrille(source, fx);
```