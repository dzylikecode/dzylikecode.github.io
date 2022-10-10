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

## Port Forwarding

端口转发命令:

- 本地端口转发到远程端口

  将本地机(客户机)的某个端口转发到远端指定机器的指定端口.

  - 工作原理

    本地机器上分配了一个 socket 侦听 port 端口, 一旦这个端口上有了连接, 该连接就经过安全通道转发出去, 同时远程主机和 host 的 hostport 端口建立连接. 可以在配置文件中指定端口的转发. 只有 root 才能转发特权端口. IPv6 地址用另一种格式说明: port/host/hostport

  ```bash
  ssh -L localSourceIP:destIP:destPort user@remotehost
  ```

  使用场景:

  - 如本地有 proxy, 远程想要通过本地的 proxy 访问网络

    1. 可以将本地的端口转发给远程的端口

       ```bash
       ssh -L 7890:destIP:5431 user@remotehost
       ```

    2. 远程配置对应的 proxy port

       ```bash
       export http_proxy=http://localhost:5431
       ```

       此时远程的 5431 端口就是本地的 7890 端口

- 远程端口转发到本地端口

  将远程主机(服务器)的某个端口转发到本地端指定机器的指定端口

  ```bash
  ssh -R remoteSourceIP:destIP:destPort user@remotehost
  ```

  - 工作原理

    远程主机上分配了一个 socket 侦听 port 端口, 一旦这个端口上有了连接, 该连接就经过安全通道转向出去, 同时本地主机和 host 的 hostport 端口建立连接. 可以在配置文件中指定端口的转发. 只有用 root 登录远程主机才能转发特权端口. IPv6 地址用另一种格式说明: port/host/hostport

- 动态端口转发

  指定一个本地机器 "动态的" 应用程序端口转发

  ```bash
  ssh -D listenPort user@remotehost
  ```

  - 工作原理

    本地机器上分配了一个 socket 侦听 port 端口, 一旦这个端口上有了连接, 该连接就经过安全通道转发出去, 根据应用程序的协议可以判断出远程主机将和哪里连接. 目前支持 SOCKS4 协议, 将充当 SOCKS4 服务器. 只有 root 才能转发特权端口. 可以在配置文件中指定动态端口的转发.

- command line options

  -C: 压缩数据传输.

  -f: 后台认证用户/密码,通常和-N 连用,不用登录到远程主机.

  -N: 不执行脚本或命令,通常与-f 连用.

  -g: 在-L/-R/-D 参数中,允许远程主机连接到建立的转发的端口,如果不加这个参数,只允许本地主机建立连接.\

  -p :被登录的 ssd 服务器的 sshd 服务端口.

### 内网穿透

- 条件

  有公网 ip 的服务器

实践部分

- [ ] 替换成 iPad 连接校园网内的 PC

(1)只有树莓派和服务器

1. 在树莓派上,通过远程端口映射,将服务器的 2222 端口映射到树莓派的 22 端口:

`ssh -fNR 2222:localhost:22 root@公网 IP`

2. 服务器上访问树莓派:

`ssh -p 2222 pi@localhost`

但事实上,有时候我们可能更需要另一个设备可以访问树莓派,而不是在服务器上访问.因此这个时候我们就需要做两次映射.

(2)树莓派,服务器,第三方设备

1. 在树莓派上,通过远程端口映射,将服务器的 2222 端口映射到树莓派的 22 端口:

`ssh -fNR 2222:localhost:22 root@公网 IP`

2. 在第三方设备上,通过本地端口映射,将第三方设备的 2222 端口映射到服务器的 2222 端口:

`ssh -fNL 2222:localhost:2222 root@公网 IP`

3. 在第三方设备上访问树莓派

`ssh -p 2222 pi@localhost`

## reference

- [OpenSSH](https://en.wikipedia.org/wiki/OpenSSH)
- [SSH port forwarding - Example, command, server config](https://www.ssh.com/academy/ssh/tunneling/example)
- [外网 SSH 连接内网 Windows 上 linux 虚拟机](https://xumingmingming.github.io/2019/06/28/linux/wai-wang-ssh-lian-jie-nei-wang-windows-shang-linux-xu-ni-ji/)
- [自建服务器解决外网访问内网的端口穿透映射](https://blog.mimvp.com/article/28549.html)
- [How to Set up SSH Tunneling (Port Forwarding)](https://linuxize.com/post/how-to-setup-ssh-tunneling/#:~:text=Dynamic%20port%20forwarding%20allows%20you,port%20on%20the%20destination%20machine.)
- [SSH Tunneling (Port Forwarding) 详解](https://johnliu55.tw/ssh-tunnel.html)
