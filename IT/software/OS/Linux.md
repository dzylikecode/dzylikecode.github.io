# centos

## graphic

- 前提

  使用 tabby 的终端

- remote

  > - command : `yum groupinstall "X Window System" -y `

- local

  > 打开 x11 forwarding 即可

## audio

[Forwarding audio like X in SSH](https://superuser.com/questions/231920/forwarding-audio-like-x-in-ssh)

## reference

[how to use xming](https://wiki.centos.org/zh/HowTos/Xming)

## 添加镜像源

- [How to Set Up and Use Yum Repositories on CentOS 7](https://linuxhostsupport.com/blog/how-to-set-up-and-use-yum-repositories-on-centos-7/)

- [How to install and enable EPEL repository on a CentOS/RHEL 7](https://www.cyberciti.biz/faq/installing-rhel-epel-repo-on-centos-redhat-7-x/)
- 查看

`yum repolist all`

- 打开

`sudo yum-config-manager --enable repository EPEL for redhat/centos 7 - x86_64`

### httping

[install](https://www.zip358.com/2015/07/26/httping%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E6%96%B9%E6%B3%95%E3%80%82centos7.html)

- test `httping localhost:7890 -g https://www.youtube.com`

## proxy

- use `port forwarding`

  > - use command line
  > - use `tabby terminal`
  >   > 通过远程端口转发到本地端口,使用本地端口代理
  >   > `ssh -R <remote_port>:localhost:<local_port> <remote_host>`
  >   >
  >   > 在`.bashrc`文件中配置
  >   >
  >   > `export http_proxy=http://localhost:<remote_port>`

- notice

> 使用端口转发需要先连接远程主机 ssh

- use frp

## frp vs port forwarding

- frp

> 可以直接通过`公网ip:指定端口`访问,不过需要开放端口

- ssh

> 先 ssh 连接,然后通过连接转发的端口
