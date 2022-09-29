# 包

- Every program is called a package.
- Package manager manages all you packages, that is installs and uninstalls them for you.
- To be able to do this, package managers holds a database of installed and available packages.

## 包管理

- 搜索包

  ```bash
  apt search <package name>
  ```

  > 一般信息有点大, 需要结合 `grep` 来使用

  ```bash
  apt search <package name> | grep -i <keyword>
  ```

- 卸载

  ```bash
  sudo apt remove <package>
  ```

- 完全卸载

  包括个人数据

  ```bash
  sudo apt purge <package>
  ```

- 删除依赖

  ```bash
  sudo apt autoremove
  ```

- 查看指定包的信息

  ```bash
  apt show <package>
  ```

  ```bash
  apt list -a <package>
  ```

> 推荐使用`apt`: It is intended as an end user interface and enables some options better suited for interactive usage by default compared to more specialized APT tools like apt-get(8) and apt-cache(8).

## 数据库

数据库中的每个包都具有状态, 指示是否安装了软件包, 软件包是否可以更新, 以及其它

- 查看当前安装的软件包

  ```bash
  dpkg -l
  ```

- 查看状态

  ```bash
  sudo apt-cache policy <package>
  ```

## reference

- [Debian package management](https://www.debian.org/doc/manuals/debian-reference/ch02.en.html)
