# bash

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

## 退出状态

```bash
echo $?
```
