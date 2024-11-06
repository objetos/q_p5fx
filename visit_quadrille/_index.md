---
bookCollapseSection: true
title: "visitQuadrille(args)"
weight: 2
draft: false
---

The `visitQuadrille` p5 function is designed to iterate over `quadrille` cells and execute a specified `fx` function on each cell. It provides a concise, less error-prone approach that aligns well with functional programming principles.

## Manual Iteration Using Nested Loops

The first and most familiar way to iterate over a `quadrille` is with standard `for` loops, a common method used for looping through matrices:

```js
for (let row = 0; row < quadrille.height; row++) {
  for (let col = 0; col < quadrille.width; col++) {
    fx(row, col);
  }
}
```

This approach, while widely understood, requires precise indexing of `row` and `col`, which can sometimes lead to errors, particularly in setting index limits.

## Iteration Using `for...of` with Cell Objects

As a more modern approach, `quadrille` cells can also be visited using a [for...of loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of) since a `quadrille` is an [iterable object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol). Here, each `cell` is an object with `value`, `row`, and `col` properties, enabling direct access to each cell’s position:

```js
for (let cell of quadrille) {
  fx(cell.row, cell.col);
}
```

This method simplifies access to `row` and `col` without explicit indexing, reducing errors. However, it still requires manual iteration logic, which can become complex in more intricate operations.

## Using `visitQuadrille` for Simplified, Less Error-Prone Iteration

The `visitQuadrille` function, a [p5.js](https://p5js.org/) utility, enhances iteration by executing the `fx` function across `quadrille` cells automatically. `visitQuadrille` promotes a clean, [declarative](https://en.wikipedia.org/wiki/Declarative_programming) style, minimizing the need for manual indexing and making it less error-prone.

With `visitQuadrille`, the iteration process becomes a single, straightforward call:

```js
visitQuadrille(source, fx);
```

This approach is not only concise but also supports scenarios that are prone to indexing errors. Additionally, `visitQuadrille` accepts an optional `values` array to selectively process specific cell values, adding flexibility without complicating the syntax.

Throughout this section, `visitQuadrille` will be used with modern [arrow functions](https://www.w3schools.com/js/js_arrow_function.asp) for even more concise and functional code, making it an essential tool for streamlined `quadrille` operations.