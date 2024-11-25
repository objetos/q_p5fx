---
bookCollapseSection: true
title: "drawQuadrille(args)"
weight: 3
draft: false
---

The `drawQuadrille` function is used to render a quadrille onto the canvas or a specified graphics buffer. It provides various parameters for customizing the appearance and behavior of the drawn quadrille, including cell dimensions, colors, and display styles.

## Syntax

> drawQuadrille(quadrille, [{[[cellLength]({{< relref "cell_length" >}})], [[outline]({{< relref "outline" >}})], [[outlineWeight]({{< relref "outline_weight" >}})], [[textColor]({{< relref "text_color" >}})], [[textZoom]({{< relref "text_zoom" >}})], [[textFont]({{< relref "text_font" >}})], [[x]({{< relref "x_y" >}})], [[y]({{< relref "x_y" >}})], [[row]({{< relref "row_col" >}})], [[col]({{< relref "row_col" >}})], [[values]({{< relref "values" >}})], [[graphics]({{< relref "graphics" >}})], [[origin]({{< relref "origin" >}})], [[tileDisplay]({{< relref "display_fns" >}})], [[stringDisplay]({{< relref "display_fns" >}})], [[numberDisplay]({{< relref "display_fns" >}})], [[colorDisplay]({{< relref "display_fns" >}})], [[imageDisplay]({{< relref "display_fns" >}})], [[functionDisplay]({{< relref "display_fns" >}})], [[arrayDisplay]({{< relref "display_fns" >}})], [[objectDisplay]({{< relref "display_fns" >}})]}])

## Parameters

| Parameter       | Description                                                                                           |
|-----------------|-------------------------------------------------------------------------------------------------------|
| quadrille       | Quadrille: The `quadrille` to be drawn                                                                |
| [cellLength]({{< relref "cell_length" >}}) | Number: Edge length in pixels. Default is [Quadrille.cellLength]({{< relref "cell_length" >}})        |
| [outline]({{< relref "outline" >}}) | [p5.Color](https://p5js.org/reference/#/p5.Color): Edge color. Default is [Quadrille.outline]({{< relref "outline" >}}) |
| [outlineWeight]({{< relref "outline_weight" >}}) | Number: Edge weight. Default is [Quadrille.outlineWeight]({{< relref "outline_weight" >}})            |
| [textColor]({{< relref "text_color" >}}) | [p5.Color](https://p5js.org/reference/#/p5.Color): Text color. Default is [Quadrille.textColor]({{< relref "text_color" >}}) |
| [textZoom]({{< relref "text_zoom" >}}) | Number: Text zoom level. Default is [Quadrille.textZoom]({{< relref "text_zoom" >}})                   |
| [textFont]({{< relref "text_font" >}}) | [p5.Font](https://p5js.org/reference/#/p5.Font): Specifies the font used for rendering text in cells. Default is the current p5.js font |
| [x]({{< relref "x_y" >}}) | Number: Upper-left quadrille pixel x-coordinate. Default is `0`. Takes precedence over `col`          |
| [y]({{< relref "x_y" >}}) | Number: Upper-left quadrille pixel y-coordinate. Default is `0`. Takes precedence over `row`          |
| [row]({{< relref "row_col" >}}) | Number: Upper-left quadrille row. Default is `0`                                                      |
| [col]({{< relref "row_col" >}}) | Number: Upper-left quadrille column. Default is `0`                                                   |
| [values]({{< relref "values" >}}) | [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of): Cells to be drawn. All cells are drawn if this parameter is `undefined` |
| [graphics]({{< relref "graphics" >}}) | [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): Renderer target. Default is `this` (main canvas) |
| [origin]({{< relref "origin" >}}) | Constant: Defines the reference point for drawing the quadrille. `CORNER` aligns it to the top-left corner of the canvas (default in `P2D`), and `CENTER` aligns it to the center of the canvas (default in `WEBGL`) |
| [tileDisplay]({{< relref "display_fns" >}})[^1] | Function: Renders cell contours. Default is `Quadrille.tileDisplay`                                   |
| [stringDisplay]({{< relref "display_fns" >}}) | Function: Renders strings in cells. Default is `Quadrille.stringDisplay`                              |
| [numberDisplay]({{< relref "display_fns" >}}) | Function: Renders numbers in cells as grayscale values. Default is `Quadrille.numberDisplay`          |
| [colorDisplay]({{< relref "display_fns" >}}) | Function: Renders colors in cells. Default is `Quadrille.colorDisplay`                                |
| [imageDisplay]({{< relref "display_fns" >}}) | Function: Renders images in cells. Default is `Quadrille.imageDisplay`                                |
| [functionDisplay]({{< relref "display_fns" >}}) | Function: Renders functions in cells, available only in WEBGL. Default is `Quadrille.functionDisplay` |
| [arrayDisplay]({{< relref "display_fns" >}}) | Function: Renders cells filled with arrays. No static default provided                                |
| [objectDisplay]({{< relref "display_fns" >}}) | Function: Renders cells filled with objects. No static default provided                               |

[^1]: The `tileDisplay` parameter allows implementing other [regular tilings](https://en.wikipedia.org/wiki/Euclidean_tilings_by_convex_regular_polygons#Regular_tilings) beyond the default [square tiling](https://en.wikipedia.org/wiki/Square_tiling).