# frp

内网穿透, 反向代理

- [repo](https://github.com/fatedier/frp)

## 需求

- 远程访问内网的电脑

  用 ipad 连接内网主机

## server

```ini
[common]
bind_port = <server_port>
dashboard_port= <port_for_board>
dashboard_user=<user_name>
dashboard_pwd=<passwd>
token=<what hell>
```

- 启动

  ```bash
  ./frps -c ./frps.ini
  ```

## client

```ini
[common]
server_addr =<server_ip>
server_port =<server_port>
token =<what hell>
tls_enable =true # sometimes need

[RDP] # name is not important
type = tcp # maybe http
local_ip =127.0.0.1 #本地ip, 局域网ip
local_port =3389 # for windows
remote_port =<what you like>
```

> 本地搭建的网页比如:`http://127.0.0.1:8080/`, 也是用`tcp`

- 启动

  ```bash
  ./frpc -c ./frpc.ini
  ```

- usage

通过`<server_ip>:<what you like>`访问局域网

## 代理

- frpc.ini

  客户端存在代理

  ```ini
  [common]
  http_proxy = http://127.0.0.1:port
  https_proxy =https://127.0.0.1:port
  ```

## issue

问题出现在:在云端服务器外还是有一个防火墙,需要通过网页操作打开

## 常用信息

### service

- frp software path

  ```txt
  /usr/local/frp
  ```

- 服务命令

  ```bash
  systemctl start frp

  systemctl stop frp

  systemctl restart frp

  systemctl status frp

  systemctl enable frp

  systemctl disable frp
  ```

## reference

- [一文搞懂 frp 内网穿透并搭建配置使用](https://developer.aliyun.com/article/853534)
- [frp 内网穿透反向代理实现 Windows 远程桌面连接](https://geomatlab.com/frp-windows-rdp/)
- [使用 Systemd 设置 frp 开机启动](https://notfound.cn/posts/systemd-frp/)
