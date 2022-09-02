# function

- [docsify 的配置 + 全插件列表](https://www.itrma.com/75.html)

## 描述结构

- 初衷

  为方便复制,将配置分解为可以直接复制的块

- 结构

  ```html
  <head>
    <!-- head 部分 -->
  </head>
  <body>
    <div id="app"></div>
    <script>
      /*!-- docsify 的部分 --*/
      window.$docsify = {};
    </script>
    <script src="//unpkg.com/docsify@4/lib/docsify.min.js"></script>
    <!-- body 部分 -->
  </body>
  ```

## latex

- head

  ```html
  <!-- latex -->
  <link
    rel="stylesheet"
    href="//cdn.jsdelivr.net/npm/katex@latest/dist/katex.min.css"
  />
  ```

- body

  ```html
  <!-- latex -->
  <script src="//cdn.jsdelivr.net/npm/docsify-katex@latest/dist/docsify-katex.js"></script>
  ```

## dark mode

- head

  ```html
  <!-- dark mode -->
  <link
    rel="stylesheet"
    href="//cdn.jsdelivr.net/npm/docsify-darklight-theme@latest/dist/style.min.css"
    title="docsify-darklight-theme"
    type="text/css"
  />
  ```

- body

  ```html
  <!-- dark mode -->
  <script
    src="//cdn.jsdelivr.net/npm/docsify-darklight-theme@latest/dist/index.min.js"
    type="text/javascript"
  ></script>
  ```

## copy to clipboard

- body

  ```html
  <!-- copy to clipboard -->
  <script src="//cdn.jsdelivr.net/npm/docsify-copy-code/dist/docsify-copy-code.min.js"></script>
  ```

## mind map

- 参考:[docsify-mindmap](https://github.com/up9cloud/docsify-mindmap)

- head

  ```html
  <!-- markmap is based on d3, so must load those files first. -->
  <script src="//unpkg.com/d3@3/d3.min.js"></script>
  <script src="//unpkg.com/markmap@latest/lib/d3-flextree.js"></script>
  <script src="//unpkg.com/markmap@latest/lib/view.mindmap.js"></script>
  <link
    rel="stylesheet"
    href="//unpkg.com/markmap@latest/style/view.mindmap.css"
  />
  ```

- docsify

  ```html
  <script>
    window.$docsify = {
      mindmap: {
        // https://github.com/dundalek/markmap
        markmap: {
          preset: "colorful", // or default
          linkShape: "diagonal", // or bracket
        },
      },
    };
  </script>
  ```

- body

  ```html
  <!-- markmap -->
  <script src="//unpkg.com/docsify-mindmap/dist/docsify-mindmap.min.js"></script>
  ```

## slidebar collapse

- head

  ```html
  <!-- slidebar collapse -->
  <link
    rel="stylesheet"
    href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar.min.css"
  />
  ```

- docsify

  ```html
  <script>
    window.$docsify = {
      loadSidebar: true, // 自定义侧边栏
      subMaxLevel: 3, // 子目录最大层级 not need
      sidebarDisplayLevel: 1, // 侧边栏显示层级 not need
    };
  </script>
  ```

- body

  ```html
  <!-- slidebar collapse -->
  <script src="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/docsify-sidebar-collapse.min.js"></script>
  ```

## mermaid

- head

  ```html
  <!-- mermaid -->
  <link
    rel="stylesheet"
    href="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.css"
  />
  <script src="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
  ```

- docsify

  ```html
  <script>
    var num = 0;
    mermaid.initialize({ startOnLoad: false });

    window.$docsify = {
      markdown: {
        renderer: {
          code: function (code, lang) {
            if (lang === "mermaid") {
              return (
                '<div class="mermaid">' +
                mermaid.render("mermaid-svg-" + num++, code) +
                "</div>"
              );
            }
            return this.origin.code.apply(this, arguments);
          },
        },
      },
    };
  </script>
  ```

## anchor

- docsify

  ```js
  window.$docsify = {
    plugins: [
      function (hook, vm) {
        hook.beforeEach(function (html) {
          return html.replace(
            /<a\s+href\s*=\s*['|"]#(.*?)['|"].*?>/gi,
            (m, g1) => m.replace(g1, vm.route.path + "#" + g1)
          );
        });
      },
    ],
  };
  ```

  目的是替换`mermaid`里面的链接

  - 副作用

    会把被反引号, txt 等包围的不是真正的 html 标签`<a href = "#anchor">`替换为`<a href = "path#anchor">`

## mermaid-latex

- head

  ```html
  <!-- mermaid-latex -->
  <script
    src="https://cdn.jsdelivr.net/npm/katex@0.10.0-rc.1/dist/katex.min.js"
    integrity="sha384-483A6DwYfKeDa0Q52fJmxFXkcPCFfnXMoXblOkJ4JcA8zATN6Tm78UNL72AKk+0O"
    crossorigin="anonymous"
  ></script>
  ```

- body

  修改`mermaid`的函数配置

  ```js
  window.$docsify = {
    markdown: {
      renderer: {
        code: function (code, lang) {
          if (lang === "mermaid") {
            let transLatex = code.replace(/c194a9ef(.*?)c194a9ef/g, (m, g1) =>
              katex.renderToString(g1).replace(/"/g, `'`)
            );
            return (
              '<div class="mermaid">' +
              mermaid.render("mermaid-svg-" + num++, transLatex) +
              "</div>"
            );
          }
          return this.origin.code.apply(this, arguments);
        },
      },
    },
  };
  ```

  - 缺点

    有些还是显示得不是很完整(有的时候, 比较奇怪, 需要多多刷新)

## search

- body

  ```html
  <!-- search -->
  <script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/plugins/search.js"></script>
  ```

## zoom image

- body

  ```html
  <!-- zoom image -->
  <script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/plugins/zoom-image.min.js"></script>
  ```

## run js code

- [doc](https://jhildenbiddle.github.io/docsify-plugin-runkit/#/)
- [repo](https://github.com/jhildenbiddle/docsify-plugin-runkit)

- head

  ```js
  window.$docsify = {
    // ...
    runkit: {
      // Options...
    },
  };
  ```

- body

  ```html
  <!-- docsify-plugin-runkit -->
  <script src="https://cdn.jsdelivr.net/npm/docsify-plugin-runkit@1"></script>
  ```
