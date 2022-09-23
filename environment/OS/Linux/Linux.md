# Linux

## 哲学

- 一切皆是文件
- 只作一件事, 尽力做好
- 通用接口, 协同运作

## vim

模态文本编辑器

- 普通模式

  移动光标, 执行删除, 复制, 粘贴, 撤销, 重做, 搜索, 替换, 保存, 退出等操作

  !> backspace 是输入文本, 不是 delete

  - 好用的命令

    `x`: 删除光标所在的字符

    `dd`: 删除光标所在的行

    `yy`: 复制光标所在的行

    `p`: 粘贴

    `u`: 撤销

    `:wq`: 保存并退出

    `:q!`: 不更改并退出

    `hjkl`: 上下左右

- 插入模式

  输入文本

  > `i` 进入插入模式, `Esc` 退出插入模式

## 手册

- whatis `command`

  查看手册的 section

- man `<command>`

  进入手册, 输入`h`可以查看文档的命令

  `man [num] <command>`: 查看命令的第 `num` 的 section

## 文本命令

- less

  > less is more

  `j`: 向下移动

  `k`: 向上移动

## bash

> `man -K /etc/profile`

- 执行过程

  执行参数扩展 => 执行程序

  - 执行参数扩展

    `*`: 通用符

    `{}`:

- `.profile`
- `.bashrc`
- `.bash_history`

## 文件处理

> 建议使用`-v`

- pwd
- ls

  `-t`: 时间序列

  `-r`: 反序

- cp
- mv
- rm
- touch

## bash 变量

- env

  类似于 c++的 protect, 子进程会继承

- set

  类似于私有变量

> environment variable have UPPER CASE and local variable have lower case names

- 变量生效的时间

  [Why can't I specify an environment variable and echo it in the same command line?](https://stackoverflow.com/questions/10938483/why-cant-i-specify-an-environment-variable-and-echo-it-in-the-same-command-line)

  ```bash
  SOMEVAR=BBB echo zzz $SOMEVAR zzz
  # zzz AAA zzz
  echo $SOMEVAR
  # BBB
  ```

  可以看到同一行执行的时候, `SOMEVAR=BBB`没有生效, 而是在执行完之后生效

  - 解决方法

    ```bash
    SOMEVAR=BBB sh -c 'echo zzz $SOMEVAR zzz'
    ```

## 语言设置

- 显示当前语言

  ```bash
  echo $LANG
  ```

- 显示所有语言配置

  ```bash
  locale
  ```

- 下载语言

  ```bash
  sudo dpkg-reconfigure locales
  ```

- 改变当前语言

  ```bash
  export LANG=en_US.UTF-8
  ```

## 重定向

## software

- 卸载

  ```bash
  sudo apt-get remove <package>
  ```

- 完全卸载

  包括个人数据

  ```bash
  sudo apt-get purge <package>
  ```

- 删除依赖

  ```bash
  sudo apt-get autoremove
  ```

## 权限

![](assets/2022-09-17-23-59-59.png)

- `Type`

  很多种 (最常见的是 - 为文件, d 为文件夹, 其他的还有 l, n ... 这种东西, 真正自己遇到了, 网上再搜就好, 一次性说太多记不住的).

- `User`

  后面跟着的三个空是使用 User 的身份能对这个做什么处理 (r 能读; w 能写; x 能执行; - 不能完成某个操作).

- `Group`

  一个 Group 里可能有一个或多个 user, 这些权限的样式和 User 一样.

- `Others`

  除了 User 和 Group 以外人的权限.

### 修改权限

```bash
chmod [who][how] [file]
```

- who

  u: 对于 User 修改

  g: 对于 Group 修改

  o: 对于 Others 修改

  a: (all) 对于所有人修改

- how

  +, -, =: 作用的形式, 加上, 减掉, 等于某些权限 \* r, w, x 或者多个权限一起, 比如 rx

- file

  施加操作的文件, 可以为多个
