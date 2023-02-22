# android

## termux

```bash
$ termux-setup-storage
```

此命令在 home 中创建 storage 文件夹，里面有 shared、dcim、downloads、pictures 等等链接，分别指向内部存储的相应文件夹，其中 shared 是指向内部存储的根目录

[Termux-setup-storage](https://wiki.termux.com/wiki/Termux-setup-storage)

## issue

- ['fatal: detected dubious ownership in repository at'](https://stackoverflow.com/questions/72978485/git-submodule-update-failed-with-fatal-detected-dubious-ownership-in-repositor)

  ```bash
  git config --global --add safe.directory '*'
  ```
