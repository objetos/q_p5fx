---
bookCollapseSection: true
weight: 1
draft: false
---

# Style

In this chapter, we introduce [static fields](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static) that set a global default style for all `Quadrille` instances. These fields can include properties and display functions. However, their default behaviors can be overridden by supplying corresponding parameters to the [drawQuadrille]({{< ref "draw_quadrille" >}}) and [sample](https://objetos.github.io/p5.quadrille.js/docs/visual_computing/sample/) methods, which hold higher priority.

Consider the following example:

```javascript
Quadrille.cellLength = 50;
let q1, q2;
let colorDisplay;

function setup() {
  q1 = createQuadrille(3, 4);
  q2 = createQuadrille(5, 2);
  colorDisplay = ({ value, cellLength }) => {
    noStroke();
    fill(value);
    ellipseMode(CORNER);
    ellipse(0, 0, cellLength, cellLength);
  }
}

function draw() {
  drawQuadrille(q1, { colorDisplay });
  drawQuadrille(q2, { cellLength: 200 });
}
```

In this code:

* The `q1` instance will use a [cellLength]({{< ref "cell_length" >}}) of `50` and the custom `colorDisplay` function to drawing cells that are filled with [colors](https://p5js.org/reference/#/p5.Color).
* Conversely, `q2` will be rendered with a `cellLength` of `200` while utilizing the default [colorDisplay]({{< ref "color_display" >}}) function to drawing cells that are filled with [colors](https://p5js.org/reference/#/p5.Color).