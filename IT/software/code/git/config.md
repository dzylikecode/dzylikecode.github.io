# Git

## configuration

- name and mail

  ```bash
  git config --global user.name "Firstname Lastname"

  git config --global user.email "your_email@example.com"​​
  ```

  会在`~/.gitconfig`中以如下形式输出设置文件

  ```ini
  ​​[user]
    name = Firstname Lastname
    email = your_email@example.com​​
  ```

- better print

  ```bash
  git config --global color.ui auto​​
  ```

  `~/.gitconfig`中会增加下面一行

  ```ini
  ​​[color]
    ui = auto​​
  ```

- 换行符

  - Linux

    ```bash
    git config --global core.autocrlf input
    ```

  - Windows

    ```bash
    git config --global core.autocrlf true
    ```

  - 不转化

    不推荐

    ```bash
    git config --global core.autocrlf false
    ```

## ssh

连接 GitHub

- generate key

  ```bash
  ssh-keygen -t rsa -C "your_email@example.com"
  ```

  !> 最好直接`enter`,设置密码会导致提交到时候总要密码

  id_rsa 文件是私有密钥, id_rsa.pub 是公开密钥

- test

  ```bash
  ssh -T git@github.com
  ```
