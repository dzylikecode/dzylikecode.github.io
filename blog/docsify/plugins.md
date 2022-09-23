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

### mermaid-latex

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
            let transLatex = code.replace(/\$(.*?)\$/g, (m, g1) =>
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

    ipad 上面无法正常显示公式: 使用 tab 来切换

    发现不能显示`\sqrt`符号, mermaid 的内部结构不支持

### marked-katex

- [Markdown 配置](https://docsify.js.org/#/zh-cn/markdown)

  同时阅读`docsify`源码

- [NFE - new feature (should be an extension)"](https://github.com/markedjs/marked/labels/NFE%20-%20new%20feature%20%28should%20be%20an%20extension%29)

  - [Add support for mark - highlighting words](https://github.com/markedjs/marked/issues/2563)

- [marked 官方文档](https://marked.js.org/using_pro)

- [Custom markdown blocks with marked](https://qubyte.codes/blog/custom-markdown-blocks-with-marked)

  ```js
  marked.use({
    walkTokens(token) {
      const { type, raw } = token;

      // Modify paragraph blocks beginning and ending with $$.
      if (
        type === "paragraph" &&
        raw.startsWith("$$\n") &&
        raw.endsWith("\n$$")
      ) {
        token.type = "code";
        token.lang = "mathematics";
        token.text = token.raw.slice(3, -3); // Remove the $$ boundaries.
        token.tokens.length = 0; // Remove child tokens.
      }
    },
    renderer: {
      code(code, language) {
        // Use custom mathematics renderer.
        if (language === "mathematics") {
          return renderMathematics(code);
        }

        // Use default code renderer.
        return false;
      },
    },
  });
  ```

- docsify 的 marked 的研究

  ```js
  window.$docsify = {
    markdown: function (marked, oldRenderer) {
      let renderer = {
        // block
        code: function (code, infostring, escaped) {
          return oldRenderer.code.apply(this, arguments);
        },
        blockquote: function (quote) {
          return oldRenderer.blockquote.apply(this, arguments);
        },
        html: function (html) {
          return oldRenderer.html.apply(this, arguments);
        },
        heading: function (text, level, raw, slugger) {
          return oldRenderer.heading.apply(this, arguments);
        },
        hr: function () {
          return oldRenderer.hr.apply(this, arguments);
        },
        list: function (body, ordered, start) {
          return oldRenderer.list.apply(this, arguments);
        },
        listitem: function (text, task, checked) {
          return oldRenderer.listitem.apply(this, arguments);
        },
        checkbox: function (checked) {
          return oldRenderer.checkbox.apply(this, arguments);
        },
        paragraph: function (text) {
          return oldRenderer.paragraph.apply(this, arguments);
        },
        table: function (header, body) {
          return oldRenderer.table.apply(this, arguments);
        },
        tablerow: function (content) {
          return oldRenderer.tablerow.apply(this, arguments);
        },
        tablecell: function (content, flags) {
          return oldRenderer.tablecell.apply(this, arguments);
        },
        // inline
        strong: function (text) {
          return oldRenderer.strong.apply(this, arguments);
        },
        em: function (text) {
          return oldRenderer.em.apply(this, arguments);
        },
        codespan: function (code) {
          return oldRenderer.codespan.apply(this, arguments);
        },
        br: function () {
          return oldRenderer.br.apply(this, arguments);
        },
        del: function (text) {
          return oldRenderer.del.apply(this, arguments);
        },
        link: function (href, title, text) {
          return oldRenderer.link.apply(this, arguments);
        },
        image: function (href, title, text) {
          return oldRenderer.image.apply(this, arguments);
        },
        text: function (text) {
          return oldRenderer.text.apply(this, arguments);
        },
      };
      marked.use({ renderer: renderer });
      return marked;
    },
  };
  ```

#### solution

> 已完成, PR 到 docsify-katex

- head

  ```html
  <!-- begin for docsify katex -->
  <link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/katex@0.16.2/dist/katex.min.css"
  />
  <script
    defer
    src="https://cdn.jsdelivr.net/npm/katex@0.16.2/dist/katex.min.js"
  ></script>
  <!-- the version of marked must between 2.1.0 and 4(not included) -->
  <script src="https://cdn.jsdelivr.net/npm/marked@3"></script>
  <!-- end for docsify katex -->
  ```

- body

  ```html
  <script>
    // import katex from "katex";
    // import marked from "marked";
    (function () {
      let originMarkdown = window.$docsify.markdown;
      let newMarked = marked; // version above 2.1.0
      function newMarkdown(originMarked, originRenderer) {
        // in docsify.js: `window.marked = marked;`
        // this will overwrite the marked
        // here `let newMarked = marked;` will not right
        function isFn(obj) {
          return typeof obj === "function";
        }
        const mathExtension = {
          name: "math",
          level: "inline",
          start(src) {
            let index = src.match(/\$/)?.index;
            return index;
          },
          tokenizer(src, tokens) {
            const blockRule = /^\$\$((\\.|[^\$\\])+)\$\$/;
            const inlineRule = /^\$((\\.|[^\$\\])+)\$/;
            let match;
            if ((match = blockRule.exec(src))) {
              return {
                type: "math",
                raw: match[0],
                text: match[1].trim(),
                mathLevel: "block",
              };
            } else if ((match = inlineRule.exec(src))) {
              return {
                type: "math",
                raw: match[0],
                text: match[1].trim(),
                mathLevel: "inline",
              };
            }
          },
          renderer(token) {
            if (token.mathLevel === "block") {
              return katex.renderToString(token.text, {
                throwOnError: false,
                displayMode: true,
              });
            } else if (token.mathLevel === "inline") {
              return katex.renderToString(token.text, {
                throwOnError: false,
                displayMode: false,
              });
            }
          },
        };
        const merge =
          Object.assign ||
          function (to) {
            for (let i = 1; i < arguments.length; i++) {
              const from = Object(arguments[i]);
              for (const key in from) {
                if (hasOwn.call(from, key)) {
                  to[key] = from[key];
                }
              }
            }
            return to;
          };

        let opts = originMarkdown || {};

        if (isFn(opts)) {
          opts = opts.apply(
            this, // make it right: return this.origin.code(src);
            originMarked,
            originRenderer
          ).defaults;
        } else {
          opts = merge(opts, {
            renderer: merge(originRenderer, opts.renderer),
          });
        }
        newMarked.setOptions(opts);
        newMarked.use({ extensions: [mathExtension] });

        return newMarked.parse;
      }
      window.$docsify.markdown = newMarkdown;
    })();
  </script>
  ```

- 代码说明

  - marked extension

    - name : 相当于 type
    - level: block 和 inline 的解析水平是不一样的
    - start: 提示(hint)可能开始的位置, 帮助`tokenizer`分析

      !> `?.` 有可能匹配不到, 所以要避免`undefined.index`报错

      比如代码是表示的是在遇到`$`的符号时可能开始分析

      ```txt
      There is a `$`, so $ e = mc^2 $
      ```

      tokenizer 接受到的是

      ```txt
      `$`, so $ e = mc^2 $
      ```

      因为反引号也会分割出 tokens

      下一步可能接受的是

      ```txt
      $ e = mc^2 $
      ```

    - tokenizer: 分析 tokens, 返回一个对象

      根据上面的分析, 正则表达式应该从开头开始匹配, 这样

      ```txt
      `$`, so $ e = mc^2 $
      ```

      第一个`$`才会被跳过

      - `raw`: 被替换的文本
      - `type`: 调用相应的 `render`

    - render: 渲染的时候调用

    文本是像 html 树一样分析, 一层一层往下: [示例](https://marked.js.org/using_pro#lexer)

    > 可以调试进一步理解这些函数, 变量的含义

  - docsify

    docsify 的内建的 marked 版本很低, 不支持插件, 需要 2.1.0 之后的版本合适, 而且版本 4 之后与之前的不兼容, 版本 4 不支持`marked(str)`的用法, 导致 docsify 报错(返回 marked.parse 可以解决版本 4 以上的问题)

    脚本需要插入到`docsify`的初始化和导入的`docsify.js`之间, 因为这是在进一步包装初始化

    !> docsify 里面有`window.marked = marked`, 会把它的旧版本的 marked 赋给全局, 这样会影响导入新的版本的 marked, 需要注意`newMarked = marked`的时机, 要的是新版本的 marked, 而不是内建版本的 marked

    中间一部分的代码是直接抄袭了 docsify 的源码

## dark mode

### default theme

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

### docsify-themeable

- [doc](https://docsify-darklight-theme.boopathikumar.me/#/docsifyThemeable)

- issue

  对于这个主题有点问题, 切换文章后, 会变白色主题

- head

  ```html
  <!-- docsify-themeable styles and switch light/dark-->
  <link
    rel="stylesheet"
    href="//cdn.jsdelivr.net/npm/docsify-darklight-theme@3/dist/docsify-themeable/style.min.css"
    type="text/css"
  />
  <link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple.css"
    title="light"
  />
  <link
    rel="stylesheet alternative"
    href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple-dark.css"
    title="dark"
  />
  <!-- End -->
  ```

- body

  ```html
  <!-- docsify-themeable styles and switch light/dark-->
  <script
    src="//cdn.jsdelivr.net/npm/docsify-darklight-theme@3/dist/docsify-themeable/main.min.js"
    type="text/javascript"
  ></script>

  <script
    src="//cdn.jsdelivr.net/npm/docsify-darklight-theme@3/dist/docsify-themeable/index.min.js"
    type="text/javascript"
  ></script>
  <!-- End -->
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
            /<a\s+(?:[^>]*?\s+)?href\s*=\s*(["'])#(.*?)\1.*?>/g,
            (m, g1, g2) => m.replace(g2, vm.route.path + "#" + g2)
          );
        });
      },
    ],
  };
  ```

  目的是替换`mermaid`里面的链接

  - 副作用

    会把被反引号, txt 等包围的不是真正的 html 标签`<a href = "#anchor">`替换为`<a href = "path#anchor">`

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

## docsify-tabs

- [docs](https://jhildenbiddle.github.io/docsify-tabs/#/)

- [repo](https://github.com/jhildenbiddle/docsify-tabs)

- head

  configuration: default

  ```js
  window.$docsify = {
    // ...
    tabs: {
      persist: true, // default
      sync: true, // default
      theme: "classic", // default
      tabComments: true, // default
      tabHeadings: true, // default
    },
  };
  ```

- body

  ```html
  <!-- docsify-tabs (latest v1.x.x) -->
  <script src="https://cdn.jsdelivr.net/npm/docsify-tabs@1"></script>
  ```

## highlighting

- [Language highlighting](https://github.com/docsifyjs/docsify/blob/develop/docs/language-highlight.md)

- 官网列表: [Supported languages](https://prismjs.com/#supported-languages)

  - 结构

    `C++ - cpp`

    - odeblock: cpp
    - 文件名: `prism-cpp.min.js`

- ini

  ```html
  <script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-ini.min.js"></script>
  ```

- bash

  ```html
  <script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-bash.min.js"></script>
  ```

- git

  ```html
  <script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-git.min.js"></script>
  ```

## iframe style

- head

  ```html
  <style type="text/css">
    iframe {
      display: block;
      border: none;
      height: 75vh;
      width: 100%;
    }
  </style>
  ```

## go back to top

- [repo](https://github.com/vfeskov/vanilla-back-to-top)

- head

  ```html
  <script src="https://unpkg.com/vanilla-back-to-top@7.2.1/dist/vanilla-back-to-top.min.js"></script>
  <script>
    addBackToTop({
      diameter: 56,
      backgroundColor: "rgb(255, 82, 82)",
      textColor: "#fff",
    });
  </script>
  ```

## pdf

- [repo](https://github.com/mozilla/pdf.js)
- [example](https://mozilla.github.io/pdf.js/examples/)

  - [more example](https://github.com/mozilla/pdf.js/tree/master/examples)

- [ ] 不够成熟

- head

  ```html
  <script src="//mozilla.github.io/pdf.js/build/pdf.js"></script>
  ```

- body

  ```js
  hook.doneEach(function () {
    // If absolute URL from the remote server is provided, configure the CORS
    // header on that server.
    // Prepare canvas using PDF page dimensions
    var canvas = document.querySelector("canvas.pdf");

    if (canvas == null || canvas == undefined) {
      return;
    }

    var url = window.location.origin + canvas.getAttribute("path");

    // Loaded via <script> tag, create shortcut to access PDF.js exports.
    var pdfjsLib = window["pdfjs-dist/build/pdf"];

    // The workerSrc property shall be specified.
    pdfjsLib.GlobalWorkerOptions.workerSrc =
      "//mozilla.github.io/pdf.js/build/pdf.worker.js";

    // Asynchronous download of PDF
    var loadingTask = pdfjsLib.getDocument(url);
    loadingTask.promise.then(
      function (pdf) {
        console.log("PDF loaded");

        // Fetch the first page
        var pageNumber = 1;
        pdf.getPage(pageNumber).then(function (page) {
          console.log("Page loaded");

          var scale = 1.5;
          var viewport = page.getViewport({ scale: scale });

          var context = canvas.getContext("2d");
          canvas.height = viewport.height;
          canvas.width = viewport.width;

          // Render PDF page into canvas context
          var renderContext = {
            canvasContext: context,
            viewport: viewport,
          };
          var renderTask = page.render(renderContext);
          renderTask.promise.then(function () {
            console.log("Page rendered");
          });
        });
      },
      function (reason) {
        // PDF loading error
        console.error(reason);
      }
    );
  });
  ```

- example

  使用方法

  ```html
  <canvas class="pdf" path="/path/to/pdf"></canvas>
  ```

- 简便使用

  ```html
  <a href="/path/to/pdf" target="_blank">电路图</a>
  ```
