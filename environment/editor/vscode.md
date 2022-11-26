# Visual Studio Code

## 了解与学习

### 学会搜索

- Stack overflow 和 Google
- Visual Studio Code 的 GitHub 台库有 Issues 和 wiki 页面

  通过 GitHub Wiki, 你可以了解到 visual Studio code 未来半年甚至一年的规划

### 学会提问

- 在提问之前,你有没有尝试自己去解决这个问题?有没有思考过问题的原因?有没有通过 Google、 Bing, Stack overflow 等搜索过类似的问题?有没有在 visual Studio code 的 GitHub Issues 上搜索过它是不是已知的 bug
- 对子提出的问题,一定描述详尽。如果是一个 bug,要提供可以完整复现 bug 的步骤

### 学会学习

### 自己的思考

- 如果以后遇到 code Runner 的 bug,也许—用再向笔者导求帮助了,直接发 pull request

### 知其然知其所以然

- 了解背后的原理和技术栈不仅有助于我们使用 visual Studio code 这个开发工具本身,而且可以帮助我们在日常的项目开发中了解更多的技术选型和架构设计,开阔我们的眼界

### 举一反三

- python 代码进行代码编辑、静态代码检査、调试、单元测试等功能

## 重要组件抽离出来

- Language Server Protocol (LSP) : 它是编辑器/IDE 与语言服务器之间的一种协议,可以让不同的编辑器/IDE 方便地支持各种编程语言的语言眼务器,允许开发人员在最喜爱的工具中使用各种语言来编写程序
- Debug Adapter Protocol (DAP) : DAP 与 Lsp 的目的类似,DAP 将编辑器/IDE 与不同语言的 debugger 解竊,极大地方便了编辑器/IDE 与其他 Debugger 的集成。Eclipse, Emacs, vim 等已经支持了 DAP。
- Monaco Editor: 作为 visual studio code 的核心组件

## 开源

- 代码开源

  可能一些开源项目也就停留在了这个阶段,甚至 GitHub 上的代码只是个镜像,内部会有代码控制系统,定期把代码同步到 GitHub 上,Issues 和 PUII requests 也是关闭的。然而真正的"开源"却不止于此

- issues 和 pull requests

  通过 GitHub 上的 Issues, Visual Studio code 团队可以倾听用户的反馈。在不同的时间段,都会有 visual Studio code 团队的成员对 GitHub 上的 Issue 进行分类。无论是 bug 还是 功能请求,开发团队都会指定相应的成员进一步的跟进

- 开源的开发流程

  - 每年, Visual Studio code 团队都会在 GitHub 的 wiki 上发布 Roadmap,列出一整年的规划图。

  - 每个月月初, 在产品设计十阶段, visual studio code 团队会在 GitHub 的 Issues 上发布 Iteration Plan, 列出这个月会开发的每一个功能, 基本上一个功能对应一个 GitHub 上的 Issue, 你可以看到详细的设计及 mockup。

  - 每个月月末,临近产品发布,你可以在 Endgame 上了解到 visual studio code 是如何进行产品测试与发布的

  > 在 wiki 上有

  visual studio code 不仅将代码开源, 而且整个产品的计划、设计及发布管理都是开源的:每个阶段对每个用户都是公开透明的,你不仅可以提交 Issue, 发布 Pull request, 甚至还可以参与到每个功能的设计与讨论中去

- 开源的生态

  - 插件开源
  - visual studio code 的文挡也是开源的

## 核心组件

- Electron

  开发框架

  不仅可以用它来开发编辑器, 还可以用它来开发任何跨平台桌面 Gul 应用程序

- Monaco Editor

  Monaco Editor 是一个基子浏览器的代码编辑器,支持业界主流的浏览器

- TypeScript

  相比 js 的特性:

  - 类型批注
  - 类型推断
  - 类型擦除
  - 接口
  - 枚举
  - Mixin
  - 泛型编程
  - 名字空间
  - 元组

  TypeScript 还引入了声明文件(扩展名为.d.ts)。声明文件的概念类似于 C/C++中的买文件,它可以被用子描述一个 Javascript 库或模块导出的虚拟的 TypeScript 类型。当开发者在使用第三方 javascript 库时,如果有声明文件的支持,那么开发者就可以方便获取第三方库的类型信息

- Language Server Protocol

  语言服务器(Language server)提供了诸如自动补全、定义跳转、代码格式化等与编程语言相关的功能

  Language Server Protocol (LSP)是编辑器/IDE 与语言服务器之间的一种协议, 通过 JSON-RPC 传输消息,可以让不同的编辑器/IDE 方便嵌入各种编程语言

- Debug Adapter Protocol

  DAP 是基子 json 的协议, 它抽象了开发工具与调试工具之间的通信

- Xterm.js

  集成终端是基于一个被广泛使用的开源项目 xterm.js 进行开发的

## 基本配置

- 设置为默认的编辑器

  ```bash
  sudo update-alternatives --set editor /path/to/vscode
  ```

  - [Getting the default text editor used in system](https://askubuntu.com/questions/615178/getting-the-default-text-editor-used-in-system)
  - [Snap: Register code as an editor in Debian with update-alternatives](https://github.com/microsoft/vscode/issues/93046)
  - [Setting VS Code as the default text editor](https://code.visualstudio.com/docs/setup/linux#_setting-vs-code-as-the-default-text-editor)

### 设置

- user setting

  全局设置范围

- workspace settings

  工作区范围, 会覆盖全局的设置

- wsl setting

  针对子系统

有图形化设置和 json 设置, 右上角有形式相互转化的按钮

json 设置时, 编号处会提示如何设置

使用`ctrl+shift+P`打开命令面板, 输入`settings`可以快速打开设置

- open User settings(UI)
- open User settings(JSON)

针对不同的语言设置

- json

  ```json
  {
    "[javascript]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    }
  }
  ```

- UI

  使用`@`, 例如`@lang:javascript`

### 快捷键

- `ctrl+P`

  文件跳转, 切换

- `ctrl+shift+o`

  寻找函数名, 快速定位块

- `ctrl+g`

  快速定位行

- `alt+shift`

  然后用鼠标拖动, 可以选择一列(shift 相当于选择起始位置和终止位置)

- `alt`

  然后点击, 可以多选鼠标

- `ctrl+shift+c`

  open the new terminal

- `ctrl+b`

  关闭侧边栏

- `ctrl+\`

  侧边栏

- `ctrl+num` 或者 `alt+ARROW`

  切换侧边栏

- `ctrl+ARROW`

  跳过单词

  可以结合`shift`选择快速选中多个单词

- `ctrl+x`

  可以用来删除整行(剪切), 不用选中任何

- `alt+shift+ARROW`

  复制选中的行(包括多行)

- `ctrl+d`

  选中下一个与选中相同的单词

- `alt+ARROW`

  将当前行与上下行进行交换

### skill

- 创建深层次文件

  `hello/test.py`, 可以连同文件夹一起创建

### 插件

- translate

  - Comment Translate

- markdown

  - Markdown All in One
  - Paste Image

- format

  - Prettier - Code formatter

    配合保存时自动格式化代码

- auto

  - GitHub Copilot
  - Tabnine AI

- web

  - Live Server

- wsl

  - Remote - WSL

- pretty

  - Material Icon Theme

  - Image preview

- js

  - auto rename tag

    vscode 内建`Linked Editing`

- live server

  当 wsl 没有浏览器的时候, 它会打开 Windows 的浏览器

尝试

- Markdown+Math
- mini-translate
- Sourcery
- Todo Tree
- Translator
- Markdown Mind Map Preview
- Ultra Math Preview for VS Code
- live preview

### 卸载

- 使用 geek 卸载后执行以下步骤

  - `win + r` 打开运行
  - `%appdata%` 回车
  - 删除 `Code` 和 `Visual Studio Code` 文件夹
  - 地址栏输入 `%userprofile%` 回车
  - 删除 `.vscode` 文件夹

## reference

- Visual Studio Code 权威指南 by 韩骏
