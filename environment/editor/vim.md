# vim

neovim

- `u`: undo
- `Ctrl+r`: undo the undos
- `Ctrl+[`: jump in
- `Ctrl+o`: jump out
- `:x`: close
- `x`: delete
- `K`: show help for word under cursor

`i` insert text `<Esc>` insert before the cursor.

`A` append text `<Esc>` append after the line.

`a` append text after the cursor

---

operator + motion

- `dw`: delete word
- `de`: delete

  current character to the end of the word

- `d$`:

  to the end of the line

- `w`: skip a word
- `e`: skip to the end of the word
- `$`: to the end of line

---

number means repeating an operator many times

`0`: the start of the line

---

`r<char>`: replace the current with `<char>`

- [ ] lesson 3.3

## key map

- [Which are the vim key notations?](https://askubuntu.com/questions/567499/which-are-the-vim-key-notations)

- `<C w w>`: switch between windows

## plug

recommend [vim-plug](https://github.com/junegunn/vim-plug)

- [installation](https://github.com/junegunn/vim-plug#installation) for vim-plug

edit `~/.config/nvim/init.vim`

- [example](https://github.com/junegunn/vim-plug#example) for installing

---

为了帮助管理文件内容, 可以将`init.vim`分割为几个内容

比如 vim-plug 可以单独创建一个文件

```bash
nvim ~/.config/nvim/vim-plug/plugins.vim
```

然后在`init.vim`里面添加

```vim
source $HOME/.config/nvim/vim-plug/plugins.vim
```

良好的文件管理: [Neovim - Setting Up VSCode Intellisense with CoC [LSP]](https://www.youtube.com/watch?v=OXEVhnY621M)

### install plugin

```vim
call plug#begin('~/.config/nvim/autoload/plugged')
<<<<<<< HEAD
Plug 'neoclide/coc.nvim', {'branch': 'release'}
=======
  Plug 'neoclide/coc.nvim', {'branch': 'release'}
>>>>>>> master
call plug#end()
```

launch nvim

```bash
nvim
:PlugInstall
:UpdateRemotePlugins
:q!
:q!
```

### remove plugin

If you want to delete a plugin:

Remove the line from your config,
Quit and restart Vim, and then
Run :PlugClean. You will be prompted to delete the directory, type Y.

## coc

创建`coc.vim`到专门的文件夹

```bash
nvim ~/.config/nvim/plug-config/coc.vim
```

复制官网给的配置[example](https://github.com/neoclide/coc.nvim#example-vim-configuration)

- config `coc`: `:CocConfig`

## window

https://www.baeldung.com/linux/vim-windows

o: 可以原地打开
