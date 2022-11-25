# zsh

## install

- install zsh

  ```bash
  sudo apt-get install zsh
  ```

- install oh-my-zsh

  ```bash
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
  ```

- install font

  `git clone https://github.com/powerline/fonts.git`

  > 觉得没有必要, I prefer the default theme

- update

  ```bash
  omz update
  ```

## plugin

1. 打开本地的路径

   ```bash
   cd ~/.oh-my-zsh/custom/plugins
   ```

   或者

   ```bash
   cd ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins
   ```

2. 在此目录下, clone the plugin
3. 编辑`.zshrc`文件, 在`plugins`中添加插件

   ```bash
   plugins=(git thePlugin1 thePlugin2)
   ```

### reference

- [Setting up Windows Subsystem for Linux with zsh + oh-my-zsh + ConEmu](https://blog.joaograssi.com/windows-subsystem-for-linux-with-oh-my-zsh-conemu/)
- [oh my zsh 插件安装详细教程及常用插件](https://segmentfault.com/a/1190000039860436)
- [WSL + oh my zsh 更好看的 shell](https://zhuanlan.zhihu.com/p/68336685)
- [Mac 下 oh-my-zsh 的安装配置和卸载](https://blog.csdn.net/s18438610353/article/details/103461470)
- [oh-my-zsh：让终端飞](https://zhuanlan.zhihu.com/p/62501175)

## issue

- `source:1: no such file or directory`

  原因是换行符的问题, 使用 git clone 的时候, 会自动转换换行符, 从而导致错误

  改用 Linux 换行符风格即可解决问题

  - [Mac 终端 zsh 安装插件时遇到的问题 `source:1:` no such file or directory: zsh-autosuggestions.zsh^M 解决办法](https://blog.csdn.net/lilyssh/article/details/118210229)
