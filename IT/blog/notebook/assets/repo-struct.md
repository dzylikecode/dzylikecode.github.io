# the structure of a repository

一个文件夹是一个包,可以在多个仓库中随意移动

一个 markdown 也是一个包

## branch

分支应该有自己明确的功能含义

- master

  > 要求尽可能的简洁
  >
  > 主分支, 最终显示

- dev

  > 用来对接 master

- doc

  > 如果 ipad clone 仓库, 则应该克隆 doc 分支, 然后新建一个 `doc-<feature>` 分支
  >
  > 所有 markdown 都在这编写

- doc-dev

  > 用来对接 doc 分支

- local-show

> 用来本地显示效果, 为了测试

- temp

> 用来存放一些细微的变化, 和下一次大的更新合并

做笔记时候的从 doc 新建一个分支,完成后推送,在电脑端检查并合并 doc

用下面的合并方式

`git merge --squash`

深入理解后,再合并, 做大的更新

目录层级不宜太深

## file struct

readme 应该是稳定的 一般作为笔记的框架和纲要

然后往外扩充
