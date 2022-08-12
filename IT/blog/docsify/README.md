# docsify

- repository: https://github.com/docsifyjs/docsify
- tutorial: https://docsify.js.org/#/quickstart

## template

### simple

- configuration

  - `.gitignore`

    ```gitignore
    # metion
    .configs/
    .Archive/
    .markeditor/
    .metion/
    .markdown/
    .sync/
    .idea/
    .DS_STORE
    Thumbs.db*
    /.posts_info.json
    /posts_info.json
    /.git_settings.json
    /git_settings.json
    /.ios_file_manager_status*.json
    /.farbox_token.*
    /.farbox_auto_sync.*
    /__wechat.json
    /*.sqlite3
    .db/
    # vs code
    .vscode/
    ```

- step

  - execute command

    ```bash
    docsify init ./docs
    ```

  - copy below to `index.html`

[](simple.html ":include :type=code html")

## 增强语法

- [嵌入文件](https://angry-swanson-b4e47b.netlify.app/embed-files)

  - 显示内容 => `[filename](_media/example.md ':include')`
  - 支持不同类型

    - iframe => .html, .htm

      `[filename](_media/example.md ':include :type=iframe')`

    - markdown => .markdown, .md
    - audio => .mp3
    - video => .mp4, .ogg
    - code => other file extension

  - 显示代码块 => `[](_media/example.html ':include :type=code js')`
  - 设置属性 => `[cinwell website](https://cinwell.com ':include :type=iframe width=100% height=400px')`

## watchlist

- Language highlighting

  - [Language highlighting](https://github.com/docsifyjs/docsify/blob/develop/docs/language-highlight.md)

  not work

- virtualize markdown as mind map

  - [使用 Markmap 将 docsify 中的 markdown 通过思维导图的形式展示出来](https://zhuanlan.zhihu.com/p/352795634)
  - [上述对应的仓库](https://gitee.com/xsro/college-notes/)
  - [docsify 如何写插件](https://docsify.js.org/#/plugins)
  - [edit 插件](https://github.com/njleonzhang/docsify-edit-on-github)
  - [参考插件](https://github.com/njleonzhang/docsify-edit-on-github/blob/master/index.js)
  - [markmap](https://github.com/gera2ld/markmap/tree/master/packages/markmap-autoloader#markmap-autoloader)

- 一个 server

  更进一步的, 我想的是只有一个 server 仓库, 其他都是文档仓库

- 运行 js

  - [将 MARKDOWN 代码块转换成可运行实例](https://smohan.net/blog/xbbqk9)
  - [markrun-docsify](https://github.com/markrun/markrun-docsify)

    总之我运行不了

  - [markrun](https://github.com/markrun/markrun)

    - [preview](https://markrun.github.io/markrun/)

      我也想实现这样的效果
