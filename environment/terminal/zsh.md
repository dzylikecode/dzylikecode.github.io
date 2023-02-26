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

```bash
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH
export PATH="$HOME/.cabal/bin:$HOME/.ghcup/bin:$PATH"
# Path to your oh-my-zsh installation.
export ZSH="$HOME/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="robbyrussell"

# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in $ZSH/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion.
# Case-sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment one of the following lines to change the auto-update behavior
# zstyle ':omz:update' mode disabled  # disable automatic updates
# zstyle ':omz:update' mode auto      # update automatically without asking
# zstyle ':omz:update' mode reminder  # just remind me to update when it's time

# Uncomment the following line to change how often to auto-update (in days).
# zstyle ':omz:update' frequency 13

# Uncomment the following line if pasting URLs and other text is messed up.
# DISABLE_MAGIC_FUNCTIONS="true"

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
# DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
# ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# You can also set it to another string to have that shown instead of the default red dots.
# e.g. COMPLETION_WAITING_DOTS="%F{yellow}waiting...%f"
# Caution: this setting can cause issues with multiline prompts in zsh < 5.7.1 (see #5765)
# COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# You can set one of the optional three formats:
# "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(git zsh-syntax-highlighting zsh-autosuggestions z)

source $ZSH/oh-my-zsh.sh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"


# DZ
export PATH=$PATH:/home/minus/.local/bin

export server_ip=$(route.exe print | grep 0.0.0.0 | head -1 | awk '{print $4}')
export dns_ip=$(cat /etc/resolv.conf | grep -oP '(?<=nameserver\ ).*')
export host_ip=$(ifconfig eth0 | grep -Po '(?<=inet )\S+')

# proxy
export https_proxy="http://${dns_ip}:10652"
export http_proxy="http://${dns_ip}:10652"
# xming
# export DISPLAY=${dns_ip}:0.0  # not need for w11
## auto set config
export xming_path='/mnt/d/Program Files (x86)/Xming/X0.hosts'
alias xconfig='echo "localhost" > "${xming_path}" && echo ${host_ip} >> "${xming_path}"'
# pulseaudio
# export PULSE_SERVER=tcp:${server_ip} # not need for w11

alias yong='sudo ssh -i /mnt/c/Users/Hasee/.ssh/id_rsa Dz@39.108.100.237'

alias ccat='pygmentize -f terminal256 -O style=native -g'
alias bdnetdisk='/opt/baidunetdisk/baidunetdisk'
export cpp_link='/home/minus/git_workspace/linux-helper/package/command/README.md'

export npm_config_proxy=${https_proxy}

export NVM_DIR="/home/minus/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/minus/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/minus/miniconda3/etc/profile.d/conda.sh" ]; then
        . "/home/minus/miniconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/minus/miniconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<

# Netcore
# https://stackoverflow.com/questions/71251998/the-required-library-libhostfxr-so-could-not-be-found-netcore-linux
export PATH=$PATH:$HOME/.dotnet/tools
export DOTNET_ROOT=$HOME/.dotnet
export PATH=$PATH:$DOTNET_ROOT

[[ "$TERM_PROGRAM" == "vscode" ]] && . "$(code --locate-shell-integration-path zsh)"

export PATH="/home/$USER/.local/bin:$PATH"
eval $(thefuck --alias)
```
