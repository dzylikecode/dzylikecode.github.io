# 系统

## 内核

> 它是应用程序和硬件级别上进行的实际数据处理之间的桥梁.内核的职责包括管理系统的资源(硬件和软件组件之间的通信).通常,作为操作系统的基本组件,内核可以为资源(特别是处理器和 I/O 设备)提供最底层的抽象,应用软件必须控制它来执行其功能.它通常通过进程间通信机制和系统调用,使这些设施可用于应用程序进程

- dmesg - 打印或控制内核环缓冲区
- /var/log/dmseg - Debian 发行版中的日志文件,仅包含系统引导期间的 dmesg 消息副本,而不包含时间戳.
- /var/log/kern.log - Debian 发行版中的日志文件,包含所有 dmesg 消息的副本,包括时间戳请注意,rsyslog 日志守护进程启动后,这个时间戳开始变- 化,这意味着 rsyslog 启动前,所有引导时的消息将具有相同的时间戳.此文件本身包含/var/log/dmseg.
- /var/log/messages - Debian 发行版中的日志文件,记录所有非调试和非关键消息.它本身包含/var/log/dmesg.
- /var/log/syslog - Debian 发行版中的日志文件,记录了所有信息,但权限相关的信息除外.它包含/var/log/messages 和/var/log/kern.log 中的所- 有消息.

## 系统启动

### 启动过程

- YOU

  Press power switch (or start a virtual machine)

  Now computer has the control

  This control is passed to BIOS

- BIOS

  Performs hardware-specific tasks

  Makes POST, Power-On Self-Test, which tests your hardware

  Detects installed hardware, such as hard disks, memory type and amount, ...

  Initializes hardware by writing initial values into their memory

  Finds a boot device, which is usually a hard disk

  Read and executes MBR (Main Boot Record) located at the beginning of this disk

  Control is not passed to MBR

- MBR

  MBR finds and executes GRUB (Grand Unified Bootloader)

  Control is now passed to GRUB

- GRUB

  Finds available filesystems

  Finds and reads its configuration file, to find out:

  Where system is located

  What system to boot

  What other actions perform

  Executes Linux Kernel, main part of Linux OS

  Control is now passed to Linux Kernel

- Linux Kernel

  Finds and loads initrd, which is initial ram disk

  initrd contains necessary drivers which allow to access and mount real filesystems

  Mounts the root file system, which is specified in GRUB config file

  Executes /sbin/init, a special program which starts all the others

  Control is now passed to init

- init

  Looks at the /etc/inittab to determine desired run level

  Loads all programs appropriate for this runlevel

  All programs from /etc/rc.d/rc2.d/ are loaded, because 2 is default Debian runlevel

  SSH and TTY are started so you are able to connect to your computer

  Booting up is now finished

- YOU

  Connect to your computer using SSH

  SSH daemon executes bash shell for you

  You can now type stuff

  You are in control once again

### 术语

- 守护进程

  无论是否登录系统, 一直运行在后台的程序

- 运行级别

  系统运行模式, 提供给 init 程序, 选择启动哪些守护程序

## 系统性能

- `uptime` - 系统运行了多长时间.
- `free` - 显示系统中可用和使用的内存量.
- `vmstat` - 进程,内存,分页,块 IO,陷阱,磁盘和 cpu 活动的信息.
- `top` - 实时显示 Linux 任务.

```bash
user1@vm1:~$ vmstat -S M
procs -----------memory---------- ---swap-- -----io---- -system-- ----cpu----
#(1,2)  (3)    (4)    (5)   (6)    (7)   (8)   (9)  (10) (11) (12,13,14,15,16)
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa
 0  0      0    229     27    196    0    0     0     0   11    6  0  0 100  0

user1@vm1:~$ vmstat -S M -a
#                    (17)    (18)
procs -----------memory---------- ---swap-- -----io---- -system-- ----cpu----
 r  b   swpd   free  inact active   si   so    bi    bo   in   cs us sy id wa
 0  0      0     11    434     19    0    0    24     2   11    6  0  0 100  0

user1@vm1:~$ vmstat -d
#19    (20)    (21)    (22)    (23)  (24)    (25)    (26)    (27)   (28)    (29)
disk- ------------reads------------ ------------writes----------- -----IO------
       total merged sectors      ms  total merged sectors      ms    cur    sec
sda    11706    353  402980   17612   9303  40546  336358   46980      0     19
sr0        0      0       0       0      0      0       0       0      0      0
loop0      0      0       0       0      0      0       0       0      0      0

user1@vm1:~$ vmstat -m | head
#(30)                       (31)  (32)   (33)   (34)
Cache                       Num  Total   Size  Pages
ext3_inode_cache          13700  13700    808     10
ext3_xattr                    0      0     88     46
journal_handle              170    170     24    170
journal_head                 37     72    112     36
revoke_table                256    256     16    256
revoke_record               128    128     32    128
kmalloc_dma-512               8      8    512      8
ip6_dst_cache                16     24    320     12
UDPLITEv6                     0      0   1024      8
```

<div>
  <table>
    <tbody>
      <tr>
        <th>Mode</th>
        <th>Stats</th>
        <th>Field</th>
        <th>Description</th>
      </tr>
      <tr>
        <td rowspan="18">Virtual memory</td>
        <td rowspan="2">Procs</td>
        <td>
          <strong>(1)</strong>
        </td>
        <td>r: The number of processes waiting for run time.</td>
      </tr>
      <tr>
        <td>
          <strong>(2)</strong>
        </td>
        <td>b: The number of processes in uninterruptible sleep.</td>
      </tr>
      <tr>
        <td rowspan="6">Memory</td>
        <td>
          <strong>(3)</strong>
        </td>
        <td>swpd: the amount of virtual memory used.</td>
      </tr>
      <tr>
        <td>
          <strong>(4)</strong>
        </td>
        <td>free: the amount of idle memory.</td>
      </tr>
      <tr>
        <td>
          <strong>(5)</strong>
        </td>
        <td>buff: the amount of memory used as buffers.</td>
      </tr>
      <tr>
        <td>
          <strong>(6)</strong>
        </td>
        <td>cache: the amount of memory used as cache.</td>
      </tr>
      <tr>
        <td>
          <strong>(17)</strong>
        </td>
        <td>inact: the amount of inactive memory.</td>
      </tr>
      <tr>
        <td>
          <strong>(18)</strong>
        </td>
        <td>active: the amount of active memory.</td>
      </tr>
      <tr>
        <td rowspan="2">Swap</td>
        <td>
          <strong>(7)</strong>
        </td>
        <td>si: Amount of memory swapped in from disk (/s).</td>
      </tr>
      <tr>
        <td>
          <strong>(8)</strong>
        </td>
        <td>so: Amount of memory swapped to disk (/s).</td>
      </tr>
      <tr>
        <td rowspan="2">I/O</td>
        <td>
          <strong>(9)</strong>
        </td>
        <td>bi: Blocks received from a block device (blocks/s).</td>
      </tr>
      <tr>
        <td>
          <strong>(10)</strong>
        </td>
        <td>bo: Blocks sent to a block device (blocks/s).</td>
      </tr>
      <tr>
        <td rowspan="2">System</td>
        <td>
          <strong>(11)</strong>
        </td>
        <td>in: The number of interrupts per second, including the clock.</td>
      </tr>
      <tr>
        <td>
          <strong>(12)</strong>
        </td>
        <td>cs: The number of context switches per second.</td>
      </tr>
      <tr>
        <td rowspan="4">CPU</td>
        <td>
          <strong>(13)</strong>
        </td>
        <td>
          us: Time spent running non-kernel code. (user time, including nice
          time)
        </td>
      </tr>
      <tr>
        <td>
          <strong>(14)</strong>
        </td>
        <td>sy: Time spent running kernel code. (system time)</td>
      </tr>
      <tr>
        <td>
          <strong>(15)</strong>
        </td>
        <td>
          id: Time spent idle. Prior to Linux 2.5.41, this includes IO-wait
          time.
        </td>
      </tr>
      <tr>
        <td>
          <strong>(16)</strong>
        </td>
        <td>
          wa: Time spent waiting for IO. Prior to Linux 2.5.41, included in
          idle.
        </td>
      </tr>
      <tr>
        <td rowspan="11">Disk, -d</td>
        <td>Device</td>
        <td>
          <strong>(19)</strong>
        </td>
        <td>Device name</td>
      </tr>
      <tr>
        <td rowspan="4">Reads</td>
        <td>
          <strong>(20)</strong>
        </td>
        <td>total: Total reads completed successfully</td>
      </tr>
      <tr>
        <td>
          <strong>(21)</strong>
        </td>
        <td>merged: grouped reads (resulting in one I/O)</td>
      </tr>
      <tr>
        <td>
          <strong>(22)</strong>
        </td>
        <td>sectors: Sectors read successfully</td>
      </tr>
      <tr>
        <td>
          <strong>(23)</strong>
        </td>
        <td>ms: milliseconds spent reading</td>
      </tr>
      <tr>
        <td rowspan="4">Writes</td>
        <td>
          <strong>(24)</strong>
        </td>
        <td>total: Total writes completed successfully</td>
      </tr>
      <tr>
        <td>
          <strong>(25)</strong>
        </td>
        <td>merged: grouped writes (resulting in one I/O)</td>
      </tr>
      <tr>
        <td>
          <strong>(26)</strong>
        </td>
        <td>sectors: Sectors written successfully</td>
      </tr>
      <tr>
        <td>
          <strong>(27)</strong>
        </td>
        <td>ms: milliseconds spent writing</td>
      </tr>
      <tr>
        <td rowspan="2">I/O</td>
        <td>
          <strong>(28)</strong>
        </td>
        <td>cur: I/O in progress</td>
      </tr>
      <tr>
        <td>
          <strong>(29)</strong>
        </td>
        <td>s: seconds spent for I/O</td>
      </tr>
      <tr>
        <td rowspan="5">Slab, -m</td>
        <td rowspan="5">Slab</td>
        <td>
          <strong>(30)</strong>
        </td>
        <td>cache: Cache name</td>
      </tr>
      <tr>
        <td>
          <strong>(31)</strong>
        </td>
        <td>num: Number of currently active objects</td>
      </tr>
      <tr>
        <td>
          <strong>(32)</strong>
        </td>
        <td>total: Total number of available objects</td>
      </tr>
      <tr>
        <td>
          <strong>(33)</strong>
        </td>
        <td>size: Size of each object</td>
      </tr>
      <tr>
        <td>
          <strong>(34)</strong>
        </td>
        <td>pages: Number of pages with at least one active object</td>
      </tr>
    </tbody>
  </table>
</div>

## reference

- [The system initialization](https://www.debian.org/doc/manuals/debian-reference/ch03.en.html)
- [Linux - top 资讯及参数说明](https://david50.pixnet.net/blog/post/45252072-%5B%E7%AD%86%E8%A8%98%5Dlinux---top%E8%B3%87%E8%A8%8A)
