# 进程

最简单的程序是硬盘上的文件, 它包含中央处理器执行的指令. 当启动它的时候,它被复制到内存,控制权传递给它. 被执行的程序称为进程. 因此可以从一个程序启动许多进程

## 进程

### 过程

- example: ls

- YOU

  Type in ls and its arguments into your terminal emulator and press `<ENTER>`

  Control is now passed to Bash

- Bash

  Locates ls on your hard disk

  Forks itself to Bash clone, that is clones itself to the new location in memory

  Becomes parent process to Bash clone

  Control is now passed to the Bash clone

- Bash clone

  Becomes child process to Bash

  Preserves parent Bash process environment

  Knows that it is it a clone and reacts accordingly

  - Overwrites itself with ls

  - Control is now passed to ls

- ls

  Prints out a directory listing for you or returns an error

  Returns exit code

  Control is now passed to Bash

- Bash

  Assigns ls exit code to ? variable

  Waits for your input

- YOU

  Are able to type something once again

### 查看进程

```bash
ps -ef
```

```bash
ps ax --forest
```

- PID: process ID
- TTY: 与进程相关联的电传模拟器,允许进程与你交换信息
- STAT: state

  ```bash
  man ps
  ```

  查阅`PROCESS STATE CODES`

- TIME

  CPU 上执行此进程的时间(单位:min)

- COMMAND

  带有参数的程序名称

### 信号

发送信号与进程沟通

```bash
kill [options] <PID>
```

## 多任务处理

- execute command in background

  ```bash
  command &
  ```

  !> 此时`command`的标准输出和标准错误输出还是会输出到终端

  - 忽略输出

    ```bash
    command > /dev/null 2>&1 &
    ```

- To **pause** and send a task to the background

  `ctrl+z`

  > `ctrl+z` stops the process and returns you to the current shell.

- to reactivate the task

  ```bash
  fg %num
  ```

- to run task in background

  bg

  ```bash
  bg %num
  ```

  > 可以使得 suspend 的任务在后台运行

- to see a list of tasks

  ```bash
  jobs
  # equls
  jobs -l
  ```

  > 会显示任务的编号和状态(suspend or running)

  - 查看文档的方法

    ```bash
    man bash
    # 然后输入
    & jobs
    ```

- to kill task in background

  ```bash
  kill %num
  ```

  or use fg command

  ```bash
  fg %num
  # then press ctrl + c
  ```

> 以上都是绑定着当前的终端

- 与终端分离

  ```bash
  disown %num
  ```

  > 无法用 jobs 查看, 参考 [Linux: View and kill disowned process](https://superuser.com/questions/1196406/linux-view-and-kill-disowned-process)

## 自动启动

cron 程序执行

- 配置文件

  ```bash
  less /etc/crontab
  ```

- 时间格式

  - `num` - 具体时间
  - `*` - 字段中的所有值,例如 分钟的`*`表示每分钟.
  - `/` - 定义范围的增量.例如,`30-40/3`意味着在第 30 分钟运行程序,每 3 分钟一次,直到第 40 分钟.
  - `%` - 在命令字段中,百分比后的所有数据将作为标准输入发送到命令.
  - `,` - 指定列表,例如分钟字段的`30,40`表示第 30 和 40 `分钟.
  - `-` - 范围.例如,分钟字段的`30-40`意味着每分钟在 30 到 40 分钟之间.
  - `L` - 指定最后一个东西,例如它允许你指定一个月的最后一天.

- 命令

  - `crontab -l` - 打印出当前的`crontab`.
  - `crontab -e` - 为当前用户编辑`crontab`.
  - `crontab -r` - 删除当前用户的`crontab`.
  - `crontab /path/to/file` - 为当前用户加载`crontab`,覆盖过程中的现有项.
  - `crontab > /path/to/file` - 将`crontab`保存到文件中.

`cron`为重复运行任务而设计,而且是很多次,并且`at`为调度一次性的任务而设计

- `at` - 在指定的时间执行命令.
- `atq` - 列出待处理的任务.
- `atrm` - 删除任务.
- `batch` - 执行命令,然后系统空转.

* example

  ```bash
  echo 'echo Here I am, sitting in ur at, staring at ur date: $(date) | write user1' | at now + 1 minutes

  atq
  ```

  ```bash
  echo '* * * * * echo Here I am, sitting in ur crontab, staring at ur date: $(date) | write user1' > ~/crontab.tmp

  crontab -l
  ```
