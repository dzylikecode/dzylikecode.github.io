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
  <script src="//cdn.jsdelivr.net/npm/docsify-katex@latest/dist/docsify-katex.js"></script>
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
    src="//cdn.jsdelivr.net/npm/docsify-darklight-theme@latest/dist/index.min.js"
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
<head>
  <!-- markmap is based on d3, so must load those files first. -->
  <script src="//unpkg.com/d3@3/d3.min.js"></script>
  <script src="//unpkg.com/markmap@latest/lib/d3-flextree.js"></script>
  <script src="//unpkg.com/markmap@latest/lib/view.mindmap.js"></script>
  <link
    rel="stylesheet"
    href="//unpkg.com/markmap@latest/style/view.mindmap.css"
  />
</head>
<body>
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

## slidebar collapse

```html
<head>
  <!--侧边栏目录展开和折叠-->
  <link
    rel="stylesheet"
    href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar.min.css"
  />
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      loadSidebar: true, // 自定义侧边栏
      subMaxLevel: 3, // 子目录最大层级 not need
      sidebarDisplayLevel: 1, // 侧边栏显示层级 not need
    };
  </script>
  <script src="//unpkg.com/docsify@4/lib/docsify.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/docsify-sidebar-collapse.min.js"></script>
</body>
```
