# 配置

克隆或创建 repo 的时候, 在`.git`的文件夹下有一个`config`文件可以查看里面的信息

## 全局配置

- name and mail

  ```bash
  git config --global user.name "Dz"

  git config --global user.email "MathBeWithCode@gmail.com"​​
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

- Change git init default branch name

  ```bash
  git config --global init.defaultBranch master
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

按照 GitHub 的说明

连接 GitHub

1. generate key

   ```bash
   ssh-keygen -t ed25519 -C "MathBeWithCode@gmail.com"
   ```

   !> 最好直接`enter`,设置密码会导致提交到时候总要密码

   id_rsa 文件是私有密钥, id_rsa.pub 是公开密钥

2. test

   ```bash
   ssh -T git@github.com
   ```

## personal

```bash
git config --global --add safe.directory '*'
```

## References

1. [Generating a new SSH key and adding it to the ssh-agent - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
