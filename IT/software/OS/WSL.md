# WSL

## reference

- [WSL2 中使用 VcXsrv 实现 xfce4 图形界面+声音传输](https://zhuanlan.zhihu.com/p/150555651)

## prepare

### some good terminals

- [windows terminal github](https://github.com/microsoft/terminal)

  > 通过`release`发布安装, 很快
  >
  > - hotkey
  >   > 首先运行 Ubuntu
  >   > Windows + ` : 呼出

- [tabby github](https://github.com/Eugeny/tabby)

### windows configuration

- search `Windows 子系统 安装`
  > 以下参考:
  >
  > - [Windows 子系统 安装](https://zhuanlan.zhihu.com/p/62658094)
  >   > 目的是打开`开发者模式`

## install

- wsl

  > 管理员模式打开`powershell`
  >
  > - 参考命令:[WSL 的基本命令](https://docs.microsoft.com/zh-cn/windows/wsl/basic-commands#set-wsl-version-to-1-or-2)
  >   > 建议安装`wsl2`, 即运行`wsl --set-default-version`
  >   >
  >   > 如果已安装`wsl1`,则可以通过`wsl --set-version Ubuntu 2`来升级

- install

  `wsl --install -d Ubuntu`

- 推荐安装过程: [Windows10/11 D 盘 安装 WSL2](https://zhuanlan.zhihu.com/p/509079404)

- 设置默认用户

  ubuntu config --default-user root

## 重装

- [Win10 系统中怎么重置 Linux 子系统?Linux 子系统重置方法](https://m.html.cn/system/windows/112633544749400.html)
  > - 可以先尝试如下方法
  >   > `wsl.exe --unregister Ubuntu`
  >   > 然后点击开始菜单里面 Ubuntu 的图标, 会重新安装

## 迁移到 D 盘

- [Windows 开启 linux 子系统并迁移到非系统盘](https://zhuanlan.zhihu.com/p/339908228)
  > - 工具:[LxRunOffline](https://github.com/DDoSolitary/LxRunOffline/releases)
  >   通过 powershell 打开到当前目录

```bash
.\LxRunOffline.exe list   #查看可用的子系统
.\LxRunOffline.exe move -n Ubuntu -d D:\WSL #将Ubuntu放在D盘的WSL文件夹下(-n指定迁移的系统，-d指定迁移路径)
.\LxRunOffline.exe get-dir #查询系统目录
```

## graphic

- [Win10 的 Linux 子系统也能运行图形程序，附详细教程](https://zhuanlan.zhihu.com/p/33312052)
- 软件:[xming](https://sourceforge.net/projects/xming/)

- for wsl-1

  > - `vim .bashrc`
  > - `export DISPLAY=127.0.0.1:0`
  > - save and execute `source .bashrc`

- for wsl-2

  > - [WSL 2: Run Graphical Linux Desktop Applications from Windows 10 Bash Shell "Error E233: cannot open display"](https://stackoverflow.com/questions/61860208/wsl-2-run-graphical-linux-desktop-applications-from-windows-10-bash-shell-erro)
  > - 注意 Windows 系统需要允许 ip 访问
  >   > 同时更改系统配置文件`(windows系统下的)`, 位于 `Xming/X0.hosts`, 需要添加 `IP`.
  >   > 其实, 可以查看 Xming 的日志, 通过右键`正在运行的 Xming` 即可找到 log 选项.
  > - 总结:
  >   > WIFI : `export DISPLAY=$(route.exe print | grep 0.0.0.0 | head -1 | awk '{print $4}'):0`
  >   > 以太网: `export DISPLAY=$(grep nameserver /etc/resolv.conf | awk '{print $2}'):0.0`

- test

  > `$ sudo apt-get x11-apps mesa-utils`
  >
  > `$ glxgears`
  >
  > `$ sudo apt-get remove --purge x11-apps mesa-utils`=>卸载

- test

  > `xdpyinfo -display <ip_address>:0.0`

- 建议安装

- gedit: `sudo apt install gedit -y`
  > 查看文件可以使用 `gedit <file_name>`

## audio

- software : [PulseAudio](https://www.freedesktop.org/wiki/Software/PulseAudio/Ports/Windows/Support/)
  > Ubuntu 对应也要安装 `sudo apt install libpulse0`
- [How To Get Sound (PulseAudio) To Work On WSL2](https://www.linuxuprising.com/2021/03/how-to-get-sound-pulseaudio-to-work-on.html)

- test

  > `sudo apt-get install paprefs`
  > 测试 `paplay --server=<ip_address>:4713 HelloWin.wav`
  >
  > - 如果是 connect failed 说明是 `export PULSE_SERVER=tcp:${hostip}` 错误
  > - 如果是 access denied, 说明是 `export PULSE_SERVER=tcp:${hostip}` 正确
  >   > 此时需要更改 `/etc/pulse/default.pa` 中的 ip 地址
  >   > 先用 `load-module module-native-protocol-tcp listen=0.0.0.0 auth-anonymous=1 `
  >   > 此时应该可以传输声音, 于是可以用 `paplay --server=tcp:${hostip}:4713 HelloWin.wav`测试一下, 然后在声音播放的同时
  >   > 在 Windows cmd 上运行 `netstat -ano | find "4713"`, 查看连接的 ip 地址
  >   > 再改回去

- issue

> - [No sound in wsl2](https://github.com/microsoft/WSL/issues/4205)

## proxy

- for wsl-1

  > vim ~/.bashrc
  > export http_proxy=http://127.0.0.1:7890
  > export https_proxy=http://127.0.0.1:7890

- for wsl-2

  > - [WSL 2 配置代理](https://solidspoon.xyz/2021/02/17/%E9%85%8D%E7%BD%AEWSL2%E4%BD%BF%E7%94%A8Windows%E4%BB%A3%E7%90%86%E4%B8%8A%E7%BD%91/)

```bash
## 获取主机 IP
## 主机 IP 保存在 /etc/resolv.conf 中
export hostip=$(cat /etc/resolv.conf |grep -oP '(?<=nameserver\ ).*')

export https_proxy="http://${hostip}:7890";
export http_proxy="http://${hostip}:7890";
```

- test
  > `curl google.com`

## language

- [WSL-gedit 中显示中文(解决中文乱码)](https://blog.csdn.net/weixin_41714373/article/details/119519589)
  > - 生成 locale 配置文件
  >   > ```bash
  >   > sudo locale-gen
  >   > locale
  >   > ```
  > - Sharing Windows fonts with WSL
  >   > ```bash
  >   > sudo apt install fontconfig
  >   > sudo vim /etc/fonts/local.conf
  >   > ```
  > - paste
  >   > ```xml
  >   > <?xml version="1.0"?>
  >   > <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
  >   > <fontconfig>
  >   >    <dir>/mnt/c/Windows/Fonts</dir>
  >   > </fontconfig>
  >   > ```

## USB

- [Connecting USB devices to WSL2](https://devblogs.microsoft.com/commandline/connecting-usb-devices-to-wsl/)
- [USB devices in WSL2](https://www.xda-developers.com/wsl-connect-usb-devices-windows-11/)
- [Connecting USB devices to WSL2](https://docs.microsoft.com/en-us/windows/wsl/connect-usb)
- [USB devices in WSL2](https://github.com/dorssel/usbipd-win)
- [USB devices in WSL2](https://version-2.com/zh/2022/02/advice-on-camera-and-microphone-in-wsl2-ubuntu/)
- [USB devices in WSL2](https://zenn.dev/pinto0309/articles/0723ae46501beb)

- [wsl](https://blog.csdn.net/qq_23301719/article/details/114027931)

`sudo apt install v4l-utils`

`sudo apt-get install cheese`

## register service

- for windows
  > - software : [NSSM](https://nssm.cc/download) > **注意**:window10 系统要下载 prerelease 版本

```bash
# 创建一个服务名称为 servicename 的服务
nssm install servicename
# 启动创建的servername服务
nssm start servicename
# 停止创建的servername服务
nssm stop servicename
# 重新启动创建的servername服务
nssm restart servicename
# 删除创建的servername服务
nssm remove servicename
```

## ssh

- [How to SSH into WSL from Windows on the same machine](https://superuser.com/questions/1123552/how-to-ssh-into-wsl-from-windows-on-the-same-machine)
- [SSH-ing into a Windows WSL Linux Subsystem](https://jeetblogs.org/post/sshing-into-a-windows-wsl-linux-subsystem/)
- [How to do SSH Connection to WSL (ubuntu) using PuTTY on Windows Tutorial](https://www.youtube.com/watch?v=7wVX-9XkasM)
- [How to Setup SSH connection on Ubuntu Windows Subsystem for Linux](https://faun.pub/how-to-setup-ssh-connection-on-ubuntu-windows-subsystem-for-linux-2b36afb943dc)
- [How to connect to Windows 10 using OpenSSH Server](https://www.youtube.com/watch?v=KLN2bY0dTtQ)
  > summary:
  > ssh port 被 Windows 占用了,需要修改服务端口.
  >
  > > 默认端口是 22,留给 Windows 使用.
  > > 如果使用 2222 端口,则`ssh -p 2222 username@hostname`
  >
  > **注意**是 `sshd_config` 而不是 `ssh_config`

## file-reference

- .bashrc

```bash
export PATH=$PATH:/home/minus/.local/bin

export server_ip=$(route.exe print | grep 0.0.0.0 | head -1 | awk '{print $4}')
export dns_ip=$(cat /etc/resolv.conf | grep -oP '(?<=nameserver\ ).*')
export host_ip=$(ifconfig eth0 | grep -Po '(?<=inet )\S+')

# proxy
export https_proxy="http://${dns_ip}:7890"
export http_proxy="http://${dns_ip}:7890"
# xming
export DISPLAY=${dns_ip}:0.0
## auto set config
export xming_path='/mnt/d/Program Files (x86)/Xming/X0.hosts'
alias xconfig='echo "localhost" > "${xming_path}" && echo ${host_ip} >> "${xming_path}"'
# pulseaudio
export PULSE_SERVER=tcp:${server_ip}


alias ccat='pygmentize -f terminal256 -O style=native -g'
alias bdnetdisk='/opt/baidunetdisk/baidunetdisk'
export cpp_link='/home/minus/git_workspace/linux-helper/package/command/README.md'
```
