# ssh

安全 Shell(SSH)是一种网络协议,用于安全数据通信,远程 Shell 服务或命令执行,以及其它两个联网计算机之间的网络服务,它们通过不安全网络上的安全通道连接:服务器和客户端(运行 SSH 服务器和 SSH 客户端程序)

- OpenSSH 是 SSH 的开源实现

  - `ssh` - 允许你连接到 SSH 服务器的客户端程序.Putty 就是这样的客户端程序.
  - `sshd` - 服务器程序,允许你使用 ssh 连接到它.
  - `/etc/ssh/ssh_config` - 默认的客户端程序配置文件.
  - `/etc/ssh/sshd_config` - 默认服务器程序配置文件.

- SSH 协议的应用

  - `scp` - 通过 SSH 传输文件.
  - `sftp` - 类似 ftp 的协议,用于管理远程文件.
  - `sshfs` - SSH 上的远程文件系统.
  - `SSH 隧道` - 一种通过安全连接,传输几乎任何数据的方法.这是非常重要的,因为它可以用于构建受保护系统的基础,以及许多其他用途.

## reference

- [OpenSSH](https://en.wikipedia.org/wiki/OpenSSH)
