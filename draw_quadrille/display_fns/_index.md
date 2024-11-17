---
bookCollapseSection: true
title: "display functions"
weight: 11
draft: false
---

## tileDisplay

Static method for drawing cell tiles.

### Example

{{< p5-global-iframe quadrille="true" width="130" height="130" >}}
'use strict';
function setup() {
  createCanvas(105, 105);
}

function draw() {
  background('yellow');
  Quadrille.tileDisplay( { graphics: this, outlineWeight: 9 } );
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
function setup() {
  createCanvas(105, 105);
}

function draw() {
  background('yellow');
  Quadrille.tileDisplay( { graphics: this, outlineWeight: 9 } );
}
```
{{< /details >}}

### Syntax

> `Quadrille.tileDisplay({graphics, [col], [row], [width], [height], [cellLength], [outline], [outlineWeight]})`

## colorDisplay

Static method for drawing cells that are filled with colors.

### Example

{{< p5-global-iframe quadrille="true" width="190" height="225" >}}
'use strict';
let color;

function setup() {
  createCanvas(165, 165);
  color = createColorPicker('magenta');
}

function draw() {
  background('blue');
  Quadrille.colorDisplay({graphics: this, value: color.value(), cellLength: width});
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let color;

function setup() {
  createCanvas(165, 165);
  color = createColorPicker('magenta');
}

function draw() {
  background('blue');
  Quadrille.colorDisplay({graphics: this, value: color.value(), cellLength: width});
}
```
{{< /details >}}

### Syntax

> `Quadrille.colorDisplay({graphics, value, [cellLength]})`

## numberDisplay

Static method for drawing cells that are filled with numbers. [Implemented](https://github.com/objetos/p5.quadrille.js/blob/main/p5.quadrille.js#L1086) in terms of [Quadrille.colorDisplay]({{< ref "color_display" >}}) as: `Quadrille.colorDisplay({ graphics: graphics, cell: graphics.color(graphics.constrain(cell, 0, 255)), cellLength: cellLength })`.

### Example

{{< p5-global-iframe quadrille="true" width="190" height="220" >}}
'use strict';
let number;

function setup() {
  createCanvas(165, 165);
  number = createSlider(0, 255, 125, 1);
}

function draw() {
  background('blue');
  Quadrille.numberDisplay( { graphics: this, value: number.value(), cellLength: width } );
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let number;

function setup() {
  createCanvas(165, 165);
  number = createSlider(0, 255, 125, 1);
}

function draw() {
  background('blue');
  Quadrille.numberDisplay({graphics: this, value: number.value(), cellLength: width});
}
```
{{< /details >}}

### Syntax

> `Quadrille.numberDisplay({graphics, value, [cellLength]})`

## stringDisplay

Static method for drawing cells that are filled with colors.

### Example

{{< p5-global-iframe quadrille="true" width="205" height="230" >}}
'use strict';
let string;

function setup() {
  createCanvas(180, 180);
  string = createInput('hola');
}

function draw() {
  background('tomato');
  Quadrille.stringDisplay({ graphics: this, value: string.value(), cellLength: width, textZoom: 0.65 });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let string;

function setup() {
  createCanvas(180, 180);
  string = createInput('hola');
}

function draw() {
  background('tomato');
  Quadrille.stringDisplay({ graphics: this, value: string.value(),
                            cellLength: width, textZoom: 0.65 });
}
```
{{< /details >}}

### Syntax

> `Quadrille.stringDisplay({graphics, value, [cellLength], [textColor], [textZoom]})`

## imageDisplay

Static method for drawing cells that are filled with [p5.Image](https://p5js.org/reference/#/p5.Image) or [p5.Graphics](https://p5js.org/reference/#/p5.Graphics) instances.

### Example

{{< p5-global-iframe quadrille="true" width="190" height="190" >}}
'use strict';
let al;

function preload() {
  al = loadImage('../abraham_lincoln.jpg');
}

function setup() {
  createCanvas(165, 165);
}

function draw() {
  background('blue');
  Quadrille.imageDisplay({ graphics: this, value: al, cellLength: width });
}
{{< /p5-global-iframe >}}

{{< details title="code" open=false >}}
```js
let al;

function preload() {
  al = loadImage('abraham_lincoln.jpg');
}

function setup() {
  createCanvas(165, 165);
}

function draw() {
  background('blue');
  Quadrille.imageDisplay({ graphics: this, value: al, cellLength: width });
}
```
{{< /details >}}

### Syntax

> `Quadrille.imageDisplay({graphics, value, [cellLength]})`

## Parameters

| parameter  | description                                                                                 |
|------------|---------------------------------------------------------------------------------------------|
| graphics   | [p5.Graphics](https://p5js.org/reference/#/p5.Graphics): renderer target                    |
| col        | Number: cell col number [\[0..width\]]({{< ref "width" >}}) default is 0                    |
| row        | Number: cell row number [\[0..height\]]({{< ref "height" >}}) default is 0                  |
| width      | Number: total number of columns default is 1                                                |
| height     | Number: total number of rows default is 1                                                   |
| cellLength | Number: edge length in pixels default is [Quadrille.cellLength]({{< ref "cell_length" >}}) |
| outline       | [p5.Color](https://p5js.org/reference/#/p5.Color) representation: edge color default is [Quadrille.outline]({{< ref "outline" >}}) |
| outlineWeight | Number: edge weight default is [Quadrille.outlineWeight]({{< ref "outline_weight" >}}). Use `0` to discard all edges |

