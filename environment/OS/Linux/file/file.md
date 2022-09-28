# 文件

## 结构

> 在 Linux 中, 所有相同类型的文件都安装在相同的位置

```bash
man hier
```

## 权限

![](assets/2022-09-17-23-59-59.png)

- `Type`

  很多种 (最常见的是 - 为文件, d 为文件夹, 其他的还有 l, n ...).

- `User`

  后面跟着的三个空是使用 User 的身份能对这个做什么处理 (r 能读; w 能写; x 能执行; - 不能完成某个操作).

- `Group`

  一个 Group 里可能有一个或多个 user, 这些权限的样式和 User 一样.

- `Others`

  除了 User 和 Group 以外人的权限.

### 修改权限

```bash
chmod [who][how] [file]
```

- who

  u: 对于 User 修改

  g: 对于 Group 修改

  o: 对于 Others 修改

  a: (all) 对于所有人修改

- how

  +, -, =: 作用的形式, 加上, 减掉, 等于某些权限 `* r, w, x` 或者多个权限一起, 比如 rx

- file

  施加操作的文件, 可以为多个
