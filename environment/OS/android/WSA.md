# WSA

## APK

- [apkpure](https://apkpure.com/cn/search?q=iA+writer&t=app)

## adb

- 查看代理

  adb shell settings get global http_proxy

- 代理

  - 连接

    adb connect 127.0.0.1:58526

  - 设置代理

    ```bash
    adb shell "settings put global http_proxy `ip route list match 0 table all scope global | cut -F3`:port"
    ```

    将 port 改为代理端口

    如果要在 powershell 里运行，请将 \` 改为 \`\`

  - 删除代理

    adb shell settings put global http_proxy :0

## issue

- adb not found

  没有添加到环境变量
