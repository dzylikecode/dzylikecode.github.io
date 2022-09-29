# 网络

## 基本概念

- [通信协议](http://en.wikipedia.org/wiki/Communications_protocol) - 通信协议,就是数字消息格式和规则的系统,用于在计算系统或在电子通讯中交换那些消息.
- [以太网](http://en.wikipedia.org/wiki/Ethernet) - 用于局域网(LAN)的计算机网络技术族.
- [MAC 地址](http://en.wikipedia.org/wiki/MAC_address) - 分配给物理网段上通信的网络接口的唯一标识符.例如:` 08:00:27:d4:45:68`.
- [TCP/IP](http://en.wikipedia.org/wiki/Internet_protocol_suite) - 互联网协议套件是一组通信协议,用于互联网和类似网络,通常是广域网最流行的协议栈.它通常被称为 TCP/IP,由于其最重要的协议:传输控制协议(TCP)和互联网协议(IP)
- [IP](http://en.wikipedia.org/wiki/Internet_Protocol) - 互联网协议(IP)是主要通信协议,用于跨互联网络中继转发数据报(也称为网络封包).
- [IP 地址](http://en.wikipedia.org/wiki/IP_address) - 互联网协议地址.示例:`10.0.2.15`
- [端口](<http://en.wikipedia.org/wiki/Port_(computer_networking)>) - 应用特定或流程特定的软件结构,在计算机的主机操作系统中用作通信端点.示例:`22`
- [网络套接字](http://en.wikipedia.org/wiki/Network_socket) - 跨计算机网络的,进程间通信流的端点.今天,大多数计算机之间的通信基于互联网协议;因此大多数网络套接字都是互联网套接字.

  套接字地址 - IP 地址和端口号,例如:`10.0.2.15:22`.

- [套接字对](http://en.wikipedia.org/wiki/Network_socket%23Socket_pairs) - 沟通本地和远程套接字,只有 TCP 协议.示例:`(10.0.2.15:22, 10.0.2.2:52173)`.
- [子网掩码](http://en.wikipedia.org/wiki/Subnetwork) - 逻辑可见的 IP 网络细分.示例:`/24`或另一个记号`255.255.255.0`.
- [路由](http://en.wikipedia.org/wiki/Routing) - 在网络中选择路径,来发送网络流量的过程.
- [默认网关](http://en.wikipedia.org/wiki/Default_gateway) - 在计算机网络中,网关是一个 TCP/IP 网络上的节点(路由器),作为另一个网络的接入点.默认网关是计算机网络上的节点,当 IP 地址与路由表中的任何其他路由不匹配时,网络软件使用它.示例:`10.0.2.2`.
- [广播地址](http://en.wikipedia.org/wiki/Broadcast_address) - 逻辑地址,其中连接到多重访问的网络的设备能接收数据报.发给广播地址的消息,通常会由所有附加到网络的主机接收,而不是特定主机.示例:`10.0.2.255`.
- [ICMP](http://en.wikipedia.org/wiki/Internet_Control_Message_Protocol) - 互联网消息控制协议,示例用法:`ping 10.0.2.2`.
- [TCP](http://en.wikipedia.org/wiki/Transmission_Control_Protocol) - 传输控制协议.在数据交换之前建立连接,因此设计上可靠.示例:SSH, HTTP.
- [UDP](http://en.wikipedia.org/wiki/User_Datagram_Protocol) - 用户数据报协议.传输数据而不建立连接,因此设计上不可靠.示例:DNS.

## 命令

- `ifconfig` - 配置和查看网络接口的状态.
- `netstat` - 打印网络连接,路由表,接口统计信息,伪装连接和组播成员资格.
- `ip` - 显示/操做路由,设备,策略和隧道.
- `ss` - 调查套接字的另一个实用程序.

- ifconfig

  查看的是 interface

  容易看到有两个 interface, `eth0`和`lo`

  > `lo` 是一个回送接口,用于连接同一台机器上的客户端-服务器程序

  |      字段      |              描述              |      字段       |             描述             |
  | :------------: | :----------------------------: | :-------------: | :--------------------------: |
  |    (1) Link    |            物理选项            |     (17) RX     |          接收(缩写)          |
  |   (2) encap    |            封装类型            |  (18) packets   |           封包总数           |
  |   (3) Hwaddr   |            MAC 地址            |   (19) errors   |       错误的数据包总数       |
  |    (4) inet    |          地址族(IPv4)          |  (20) dropped   |   丢弃的封包(低系统内存?)    |
  |    (5) addr    |           IPv4 地址            |  (21) overruns  |      比处理速度快的封包      |
  |   (6) Bcast    |            广播地址            |   (22) frame    |        接收的无效的帧        |
  |    (7) Mask    |            网络掩码            |     (23) TX     |          传输(缩写)          |
  |   (8) inet6    |          地址族(IPv6)          |  (24) packets   |           封包总数           |
  |    (9) addr    |           IPv6 地址            |   (25) errors   |       错误的数据包总数       |
  |   (10) Scope   |    地址范围(主机,链路,全局)    |  (26) dropped   |   丢弃的封包(低系统内存?)    |
  |    (11) UP     |          接口功能正常          |  (27) overruns  | 比处理速度快的封包(我不确定) |
  | (12) BROADCAST | 它可以一次性向所有主机发送流量 |  (28) carrier   |         链路载波丢失         |
  |  (13) RUNNING  |   它准备好接受数据(我不确定)   | (29) collisions |        发生了包装碰撞        |
  | (14) MULTICAST |    它可以发送和接收组播封包    | (30) txqueuelen |   传出数据包的转发队列长度   |
  |    (15) MTU    |         其最大传输单位         |  (31) RX bytes  |        收到的字节总数        |
  |  (16) Metric   |  路由开销(在 Linux 中未使用)   |  (32) TX bytes  |        发送的字节总数        |

  - 重点字段

    (5) addr - IPv4 地址.
    (6) Bcast - 广播地址.
    (7) Mask - 网络掩码.
    (11) UP - 接口正常工作.
    (13) RUNNING - 准备好接受数据.
    (19) errors 和 (25) errors - 如果在这里有不为零的东西,我们就有问题了.

- [netstat](https://www.computerhope.com/unix/unetstat.htm)

  输出两个部分

  - Output: Internet connections

  - Output: Unix domain sockets

    - Proto

      套接字使用的协议(tcp,udp,raw)

    - Local Address

      套接字本端的地址和端口号

    - Foreign Address

      套接字远端的地址和端口号, 仅用于套接字对

    - State

      - LISTEN

        可以连接到这个套接字

      - ESTABLISHED

        套接字已经连接了, 且会显示套接字对.

- [ip](https://www.computerhope.com/unix/ip.htm)

  > On many Linux systems, it replaces the deprecated ifconfig command.

- ss

  基本上是具有扩展功能的当代 netstat

- route

  - Destination - 目标网络或目标主机.
  - Gateway - 网关地址或`*`,如果没有设置的话.默认值意味着,如果没有明确指定的目标地址的网关,则将通过该网关发送数据包.
  - Genmask - 目标网络的网络掩码;255.255.255.255 为主机目标,0.0.0.0 为默认路由.
  - Iface - 用于这个路由的,发送封包的接口.

## reference

- [Linux Networking-concepts HOWTO](http://web.archive.org/web/20140405045417/http://iptables.org/documentation/HOWTO/networking-concepts-HOWTO.html#toc5)
- [Linux Networking Cookbook](https://doc.lagout.org/operating%20system%20/linux/Linux%20Networking%20Cookbook.pdf)
- [Introduction to Linux Networking](https://iq.opengenus.org/introduction-to-linux-networking/)
- [Introduction to Linux networking](https://doxfer.webmin.com/Webmin/Introduction_to_Linux_networking)
- [Linux netstat command](https://www.computerhope.com/unix/unetstat.htm)
