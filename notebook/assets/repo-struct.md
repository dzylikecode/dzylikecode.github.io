# the structure of a repository

一个文件夹是一个包,可以在多个仓库中随意移动

一个 markdown 也是一个包

## branch

- master

> 主分支, 最终显示

- doc

> 所有 markdown 都在这编写

- local-show

> 用来本地显示效果, 合理再合并到 master

做笔记时候的从 doc 新建一个分支,完成后推送,在电脑端检查并合并 doc

用下面的合并方式

`git merge --squash`

深入理解后,再合并吧

分支也有层级,就像几级目录一样,只显示到二级这样

## file struct

readme 应该是稳定的 一般作为笔记的框架和纲要

然后往外扩充
