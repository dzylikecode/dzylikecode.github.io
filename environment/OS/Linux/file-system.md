# 文件系统

## 挂载

- 磁盘分区

  将硬盘驱动器分为多个逻辑存储单元,它们被称为分区,来将一个物理磁盘驱动器视为多个磁盘

  > "分治"原则的应用, 流氓程序不能通过占用所有磁盘空间, 使整个服务器崩溃, 该程序将限制在其分区中

- 文件系统

  一种组织数据的手段

  > 类 Unix 操作系统创建一个虚拟文件系统,这使得所有设备上的所有文件似乎都存在于单个层次结构中.这意味着,在这些系统中,有一个根目录,系统上存在的每个文件位于它下方的某个地方.
  >
  > 所有文件系统都集成在一个大树中

- 查看`/etc/fstab`文件

  格式的理解, 阅读 fstab 文档

  ```bash
  man fstab
  ```

- `mount` - 打印出所有已挂载的文件系统.
- `mount -a` - 挂载/etc/fstab 中描述的所有文件系统.
- `mount /dev/sda<N> /<mount point>` - 挂载分区.
- `umount /dev/sda<N> /<mount point>` - 解除挂载分区.
- `mount -h` - 打印出使用 mount 的简短帮助.
- `fsck` - 检查分区是否有错误.
- `blkid` - 打印出唯一的分区标识符.

  需要提升权限

## 修改与创建

- 查阅文档

  man mkfs, man mkfs.ext3, man tune2fs

## 修改根目录

Unix 操作系统上的 chroot 是一个操作,可以为当前正在运行的进程及其进程修改根目录.在这种修改后的环境中运行的程序,不能指定(也就是访问)这个`特定目录树之外`的文件

## 移动数据

```bash
man tar
man dd
```

## reference

- [Filesystems: modifying and creating filesystems, tune2fs, mkfs](https://archive.ph/CzHiN#selection-225.13-225.75)
- [Filesystems: moving data around: tar, dd](https://archive.ph/JSknE#selection-225.13-225.53)
