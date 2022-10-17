# 工具

## the fuck

repo: https://github.com/nvbn/thefuck#experimental-instant-mode

1. 利用 conda 安装, 进入 conda 环境`sys`, 然后安装

   ```bash
   pip3 install thefuck --user
   ```

2. 配置 zsh

   ```bash
   export PATH="/home/$USER/.local/bin:$PATH"
   eval $(thefuck --alias)
   ```
