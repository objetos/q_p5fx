---
bookCollapseSection: true
title: "visitQuadrille(args)"
weight: 2
draft: false
---

This chapter introduces techniques for iterating over `quadrille` cells and executing a specified `fx` function on each cell. By providing flexible ways to visit cells, `visitQuadrille` supports common operations and introduces arrow functions, simplifying function expressions.

## Manual Iteration Using Nested Loops

The traditional way to visit each cell in a `quadrille` involves using nested `for` loops. Here, `row` and `col` represent the current cell’s position as `fx(row, col)` executes on each cell:

```js
for (let row = 0; row < quadrille.height; row++) {
  for (let col = 0; col < quadrille.width; col++) {
    fx(row, col);
  }
}
```

## Iteration Using `for...of` with Cell Objects

Since a `quadrille` is an [iterable object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol), cells can also be visited with a [for...of loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of). Each `cell` is an object literal containing `value`, `row`, and `col` properties, making it possible to access cell positions directly:

```js
for (let cell of quadrille) {
  // cell is an object with value, row, and col properties
  fx(cell.row, cell.col);
}
```

## Using `visitQuadrille` for Simplified Iteration

The `visitQuadrille` function, a [p5.js](https://p5js.org/) helper, provides a streamlined way to execute the `fx` function across `quadrille` cells. By accepting `(row, col)` parameters for the cell position, it enables custom logic for each cell, allowing either all cells or only those with specific `values` to be processed.

With `visitQuadrille`, the iteration in the previous examples simplifies to:

```js
visitQuadrille(source, fx);
```

This approach reduces the need for manual loops, making code cleaner and introducing the use of concise [arrow functions](https://www.w3schools.com/js/js_arrow_function.asp) as anonymous expressions. Arrow functions offer a modern syntax, which will be demonstrated in detail in this chapter’s examples.