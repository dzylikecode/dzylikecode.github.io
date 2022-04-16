# function

- [docsify 的配置 + 全插件列表](https://www.itrma.com/75.html)

## latex

```html
<head>
  <!-- here !!!!! -->
  <link
    rel="stylesheet"
    href="//cdn.jsdelivr.net/npm/katex@latest/dist/katex.min.css"
  />
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      name: "",
      repo: "",
    };
  </script>
  <!-- Docsify v4 -->
  <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
  <!-- here !!!!! -->
  <script src="//cdn.jsdelivr.net/npm/docsify-katex@1.4.5/dist/docsify-katex.js"></script>
</body>
```

## dark mode

```html
<head>
  <!-- here !!!!! -->
  <link
    rel="stylesheet"
    href="//cdn.jsdelivr.net/npm/docsify-darklight-theme@latest/dist/style.min.css"
    title="docsify-darklight-theme"
    type="text/css"
  />
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      name: "",
      repo: "",
    };
  </script>
  <!-- Docsify v4 -->
  <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
  <!-- here !!!!! -->
  <script
    src="//cdn.jsdelivr.net/npm/docsify-darklight-theme@3.2.0/dist/index.min.js"
    type="text/javascript"
  ></script>
</body>
```

## copy to clipboard

```html
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      name: "",
      repo: "",
    };
  </script>
  <!-- Docsify v4 -->
  <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
  <!-- here !!!!! -->
  <script src="//cdn.jsdelivr.net/npm/docsify-copy-code/dist/docsify-copy-code.min.js"></script>
</body>
```

## mind map

- [docsify-mindmap](https://github.com/up9cloud/docsify-mindmap)

```html
<body>
  <!-- markmap is based on d3, so must load those files first. -->
  <script src="//unpkg.com/d3@3/d3.min.js"></script>
  <script src="//unpkg.com/markmap@0.6.1/lib/d3-flextree.js"></script>
  <script src="//unpkg.com/markmap@0.6.1/lib/view.mindmap.js"></script>
  <link
    rel="stylesheet"
    href="//unpkg.com/markmap@0.6.1/style/view.mindmap.css"
  />

  <div id="app"></div>
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
  <script src="//unpkg.com/docsify@4/lib/docsify.min.js"></script>
  <script src="//unpkg.com/docsify-mindmap/dist/docsify-mindmap.min.js"></script>
</body>
```
