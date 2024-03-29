# 想法

## docsify 支持 demo

像嵌入 jsfiddle 一样

- runkit+jsdom

  一种实现方式是用 runkit 加上[jsdom](https://github.com/jsdom/jsdom#intervening-before-parsing)模拟浏览器

  ```js
  const jsdom = require("jsdom");
  const { JSDOM } = jsdom;
  const window = new JSDOM(`<body>
  <script>document.body.appendChild(document.createElement("hr"));</script>
  </body>`).window;
  global.window = window;
  global.document = window.document;
  global.DOMParser = window.DOMParser;

  var Algebra = require("ganja.js");

  // Create a Clifford Algebra with 2,0,1 metric.
  Algebra(2, 0, 1, () => {
    // in 2D PGA, grade-1 elements or vectors (e0,e1,e2) represent
    // reflections AND lines (the invariant of a reflection)
    // Ganja.js overloads scientific notation to specify basis blades.
    var line = (a, b, c) => a * 1e1 + b * 1e2 + c * 1;

    // grade-2 elements or bivectors (e01,e02,e12) represent
    // rotations/translations AND points/infinite points (the invariant
    // of a rotation/translation). We define them using the dualisation
    // operator (!) to be independent of choice of basis (e12 vs e21)
    var point = (x, y) => !(1 + x * 1e1 + y * 1e2);

    // Define 3 points in the plane.
    var A = point(-1, -1),
      B = point(-1, 1),
      C = point(1, 1);

    // Define the line y = 0.5 - x <=> x + y - 0.5 = 0
    var L = line(1, 1, -0.5);

    // A line can also be defined by JOINING (&) two points.
    // We define M as a function '()=>' so it will update when C or A
    // are dragged.
    var M = () => C & A;

    // Similarly a point can be defined by MEETING (^) two lines.
    // Again, we define point D as a function so it will update when
    // L or M change.
    var D = () => L ^ M;

    // We now use the graph function to create an SVG object that visualises
    // our algebraic elements. The graph function accepts an array of items
    // that it will render in order. It can render points, lines, labels,
    // colors, line segments and polygons.
    document.body.appendChild(
      this.graph(
        [
          "Drag A,B,C", // First label is used as title.
          0xd0ffe1, // Numbers are colors - use hex!
          [A, B, C], // render polygon ABC.
          0x882288, // Set the color to purple.
          [B, C], // Render line segment from B to C.
          0x00aa88, // Medium green.
          L,
          "L",
          M,
          "M", // Render and label lines.
          0x224488, // Set color blue.
          D,
          "D", // Intersection point of L and M
          0x008844, // Set darker green
          A,
          "A", // Render point A and label it.
          B,
          "B", // Render point B and label it.
          C,
          "C", // Render point C and label it.
        ],
        {
          grid: true, // Display a grid
          labels: true, // Label the grid
          lineWidth: 3, // Custom lineWidth (default=1)
          pointRadius: 1, // Custon point radius (default=1)
          fontSize: 1, // Custom font size (default=1)
          scale: 1, // Custom scale (default=1), mousewheel.
        }
      )
    );
  });
  document.documentElement.innerHTML;
  ```

  但是有挺多浏览器的特性不支持, 比如 canvas, 画面刷新等

- 一个网上的效果

  https://github.com/chrisdiana/webden

- jsFiddle

  https://docs.jsfiddle.net/api/display-a-fiddle-from-post

  有点用, 但是不能嵌入

  帮助做一个按钮: https://github.com/jsfiddle/jsfiddle-post.js

- stack overflow 的实现

  https://meta.stackoverflow.com/questions/269753/feedback-requested-runnable-code-snippets-in-questions-and-answers

- python 的实现

  https://runno.dev/#examples

  repo: https://github.com/taybenlor/runno

- docsify 相同的想法

  https://github.com/docsifyjs/docsify/issues?q=+jsfiddle

- 借助

  docsify-tabs 完成

https://observablehq.com/@enkimute/ganja-js-introduction
