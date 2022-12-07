# issue

## git 默认不区分文件大小写

```bash
git config core.ignorecase false
```

- [解决 Git 默认不区分文件名大小写的问题](https://www.jianshu.com/p/df0b0e8bcf9b)

远程仓库上大写的 README.md 却没有被删除，居然同时存在了

更加坑爹的是当你把本地仓库删掉后，重新从远程仓库 clone 下来发现，还是只有小写的 readme.md 这一个文件

> 最好是重命名为其他文件提交, 然后再次重命名

直接使用 `git mv` 能够解决问题

## connection refused

### DNS pollution

[git 访问 github 失败 Connection refused 解决方案](https://www.shouxicto.com/article/5947.html)

需要权限修改

```bash
sudo vim /etc/hosts
```

添加

```bash
# GitHub
20.205.243.166  github.com
20.205.243.160  ssh.github.com
```
