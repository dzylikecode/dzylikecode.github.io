# the structure of a repository

- 不急于大的更新, 大的更新旨在较为深刻的理解

## file

- file

  - file 与 folder 等价, 作为基本单元

  - 闭包

    尽可能简单地创建为单一 markdown 文件, 如果有 assets, 则用文件夹包裹起来, 作为一个整体

- 目录

  神似思维导图

  层级不宜太深

- README

  稳定, 一般为框架, 纲要, 总结

  然后根据 README 扩充

## branch

- 初衷

  分支应该有自己明确的功能含义

  分支简洁

- 设计

  - master(remote)

    干净

  - dev

    测试

    合并到 master: `git merge --squash`

  - doc(remote)

    干净

    文档都在这

  - doc-dev

    文档编写

    合并到 dev, 测试后, 再合并到 doc: `git merge --squash`

  - `<branch_func>`

    ipad 上面功能开发

    开发完后, 合并, 删除

  - temp

    用来存放一些细微的变化, 和下一次大的更新合并
