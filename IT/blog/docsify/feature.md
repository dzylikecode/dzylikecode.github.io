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
