# ipad 上面安装 Linux

## 过程

安装 ish app

- 挂载 mount

  > - [video](https://youtu.be/e6IynTRmMQ4)
  > - key : `mount -t ios doesntmatter /mountpoint`

- 安装 git

  > - command : `apk install git`

- 安装 ssh
  > - command : `apk add openssh`

## vscode

- [VSCode on iPad Pro](https://www.youtube.com/watch?v=11YfaGi0Fpk)
- [Can you Write Code on an iPad? | Code-Server tutorial](https://www.youtube.com/watch?v=OHSAk0n3mqs)

```txt
To have systemd start code-server now and restart on boot:
 sudo systemctl enable --now code-server@$USER
Or, if you don't want/need a background service you can run:
code-server
```

## remote desktop

- [远程桌面连接失败 - 错误 0x204 或 0x207](https://social.technet.microsoft.com/Forums/systemcenter/zh-CN/d17b63af-6b62-4bd9-a426-d2be26277fdd/remote-desktop-connection-fails-error-0x204-or-0x207?forum=w8itpronetworking)

> - address: `<ip>[:<port>]` 默认是 3389
> - accout : `MicrosoftAccout\<email>`
