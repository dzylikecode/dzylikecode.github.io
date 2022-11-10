# 插件开发

## logger

```js
const vscode = require("vscode");
const moment = require("moment");
function Logger() {
  this.channel = vscode.window.createOutputChannel("Paste Image");
  this.log = (msg) => {
    if (this.channel) {
      let time = moment().format("MM-DD HH:mm:ss");
      this.channel.appendLine(`[${time}] ${msg}`);
    }
  };
  this.close = () => this.channel.dispose();
}

module.exports = new Logger();
```

## configuration

```js
port = vscode.workspace.getConfiguration("docsifyPreview").get("port");
docsifyIndexFilePath =
  vscode.workspace.getConfiguration("docsifyPreview").indexFile;
```

```ts
class Config {
  private static setSettings(
    key: string,
    val: number,
    isGlobal: boolean = false
  ): Thenable<void> {
    return Config.configuration.update(key, val, isGlobal);
  }
}
A;

await Config.setPort(Config.getPort + 1); // + 1 will be fine
```

### reference

- [prettier log](https://github.com/prettier/prettier-vscode/blob/main/src/LoggingService.ts)
