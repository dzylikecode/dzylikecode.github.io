# 文档

## man

- [Linux man pages](https://linux.die.net/man/)

### 结构

- page 结构

  - 可执行程序或 shell 命令
  - 系统调用(内核提供的函数)
  - 库调用(程序库中的函数)
  - 特殊文件(通常在/dev 中找到)
  - 文件格式和约定,例如/etc/passwd
  - 游戏
  - 其他(包括宏及惯例),例如 man(7), groff(7)
  - 系统管理命令(通常仅适用于 root 用户)
  - 内核例程`[非标准]`

查看手册的 section

```bash
whatis <command>
```

- man `<command>`

  进入手册, 输入`h`可以查看文档的命令

  `man [num] <command>`: 查看命令的第 `num` 的 section

  输入`\`然后可以输入关键字, `n`可以下一个关键字(通过查阅 help 文档可以得知)

- section

  - NAME(名称) - 程序名称和简短描述.
  - SYNOPSIS(概要) - 可用程序选项的简短列表
  - DESCRIPTION(描述) - 程序的描述和可用参数的说明.
  - OPTIONS(选项) - 一些手册页在这里继续说明可用的参数.
  - EXIT STATUS(退出状态) - 每个程序返回一个代表其成功或失败的代码.这里解释这些代码值.
  - RETURN VALUE(返回值) - 通常与退出状态相同.
  - ERRORS(错误) - 程序中已知的错误.
  - ENVIRONMENT(环境) - 环境变量.在调用程序之前设置它们.
  - FILES(文件) - 通常是程序配置文件.
  - VERSIONS(版本) - 有关程序更改的信息.
  - CONFORMING TO(适用于) - 兼容性说明.
  - NOTES(注意) - 手册的作者不知道放在哪里的信息.
  - BUGS - 程序中已知的错误.
  - EXAMPLE(示例) - 包含程序调用的示例.
  - AUTHORS(作者) - 谁写的程序.
  - SEE ALSO(另见)- 相关手册页.

- 命令结构

  - 粗体文本 - 类型完全如图所示.
  - 斜体文本 - 用适当的参数替换.这个文字大部分显示不是斜体,而是像下划线一样 .
  - `[-abc]` - []内的任何或所有参数是可选的.
  - `-a|-b` - 由|分隔的选项不能一起使用
  - `argument ...` - 参数是可重复的.
  - `[expression] ...` - []中的整个表达式是可重复的.

  - example

    ```bash
    man less
    ```

    `[-{oO} logfile]`, 整体是可选的, 如果选择, 则一定有`-`, 然后`o`或`O`选一个, 最后指定 logfile

## info

- `<UP>`, `<DOWN>`, `<LEFT>`, `<RIGHT>`可让你滚动文字.
- `<ENTER>`打开光标下的链接.链接以\*开头.
- `<TAB>` - 跳转到文档中的下一个链接.
- u - 转到上一级
- p - 转到上一页,就像浏览器一样.
- n - 转到下一页.
- q - 关闭 info.

## Google

- 使用建议

  1. Find a "how to".
  2. Follow it, but read, or at least skim, through man pages

  > Do not follow any How To blindly, ever!

### resource

- http://en.wikipedia.org

  is invaluable when getting initial information about some topic. Its links section is even more invaluable.

- http://stackexchange.com/

  This is very useful site for finding information about usage examples and use cases. StackExchange network includes several resources, of which most useful to you are http://serverfault.com/ and http://unix.stackexchange.com/.

  http://stackoverflow.com/ is a very useful resource when you are doing bash scripting.

- http://www.cyberciti.biz/ contains many useful "how to's" and examples.

- Homepages of many programs provide good and sometimes great documentation.

  For example this are for apache and ngnix, respectively: http://httpd.apache.org/docs/, http://nginx.org/en/docs/.

- http://tldp.org/

  is The Linux Documentation Project and contains many in-depth guides about different topics.

### search skills

- (screen|tmux) how to

  search for screen and tmux howtos at the same time.

- site:serverfault.com query

  search something on this site only. You may search several sites at once with (site:serverfault.com | site:stackexchange.com)

- "a long query"

  shows you only those pages which contain this query exactly.

- `-query`

  excludes something from search results.
