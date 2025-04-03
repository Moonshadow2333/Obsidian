---
aliases:
  - NPM
  - Vue
  - Node
date: 2025-03-17
---

# 目录

```dataviewjs
const startHeadinglevel = 2;
const file = app.workspace.getActiveFile();
const { headings } = app.metadataCache.getFileCache(file);
 
// 全列表的形式
const raws = headings.filter(row => row.heading != "目录").map( p => {
    let repeatCount = Math.max((p.level - startHeadinglevel) * 4, 0);
    let spacesPrefix = ' '.repeat( repeatCount + 4 );
    let listSign = repeatCount > 0 ? '- ' : '';
    let linkText = `[[#${p.heading}]]`;
    let headingList = (p.level < startHeadinglevel) ? `- ${linkText}` : `${spacesPrefix}- ${linkText}`;
    return headingList;
  }
)
 
let result = raws.join('\n');
// 添加行距
dv.container.style.lineHeight = "1.5em";
dv.paragraph(result)
```

# npm install

在本地 node_modules 文件夹中安装依赖项。

在全局模式下（即，将 `-g` 或 `--global` 附加到命令中），它将当前包上下文（即当前工作目录）安装为全局包。

默认情况下，`npm install` 将安装 [`package.json`](https://nodejs.cn/npm/cli/v6/commands/npm-install/##8f47a3c27ce24f8ba12683bc8c450434) 中列为依赖项的所有模块。

使用 `--production` 标志（或者当 `NODE_ENV` 环境变量设置为 `production` 时），npm 将不会安装 `devDependencies` 中列出的模块。当 `NODE_ENV` 环境变量设置为 `production` 时，要安装 `dependencies` 和 `devDependencies` 中列出的所有模块，您可以使用 `--production=false`。

> 注意：在向项目添加依赖项时，`--production` 标志没有特殊含义。

[npm 超详细教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/258080852)

[前端开发者需要知道的 package.json - 掘金 (juejin.cn)](https://juejin.cn/post/6969454249411837965)

# 配置全局模块路径及缓存路径

完成安装后最好配置一下npm全局模块路径和缓存路径，因为默认的npm全局模块路径和缓存路径在C盘

[Node.js的安装以及配置npm全局模块路径和缓存路径 - Caution_X - 博客园](https://www.cnblogs.com/cautx/p/17324367.html)
[（Nodejs）安装教程、切换全局模块安装路径、切换npm下载源 - 高sir不会跳舞 - 博客园](https://www.cnblogs.com/haoran5544/p/18059171)

```
# 查看配置
npm config list
; "builtin" config from D:\00Apps\15NodeJs\node_modules\npm\npmrc

prefix = "C:\\Users\\Moonshadow2333\\AppData\\Roaming\\npm"

; node bin location = D:\00Apps\15NodeJs\node.exe
; node version = v22.12.0
; npm local prefix = C:\Users\Moonshadow2333
; npm version = 10.9.0
; cwd = C:\Users\Moonshadow2333
; HOME = C:\Users\Moonshadow2333
; Run `npm config ls -l` to show all defaults.

# 修改

# 首先设置全局安装位置 命令：
C:\Users\Moonshadow2333>npm config set prefix "D:\00Apps\09Node\NodeJs\node_global"

# 接下来设置缓存安装位置 命令：
C:\Users\Moonshadow2333>npm config set cache "D:\00Apps\09Node\NodeJs\node_cache"

# 再次查看配置
C:\Users\Moonshadow2333>npm config list
; "builtin" config from D:\00Apps\09Node\NodeJs\node_global\node_modules\npm\npmrc

; prefix = "C:\\Users\\Moonshadow2333\\AppData\\Roaming\\npm" ; overridden by user

; "user" config from C:\Users\Moonshadow2333\.npmrc

cache = "D:\\00Apps\\09Node\\NodeJs\\node_cache"
prefix = "D:\\00Apps\\09Node\\NodeJs\\node_global"

; node bin location = D:\00Apps\15NodeJs\node.exe
; cwd = C:\Users\Moonshadow2333
; HOME = C:\Users\Moonshadow2333
; Run `npm config ls -l` to show all defaults.

# 修改环境变量
原 C:\Users\Moonshadow2333\AppData\Roaming\npm
新 D:\00Apps\09Node\NodeJs\node_global
```

# 查看已经安装过的包

```cmd
npm ls --depth 0
```

# 文档

[卸载包和依赖 - npm 中文文档](https://nodejs.cn/npm/packages-and-modules/getting-packages-from-the-registry/uninstalling-packages-and-dependencies/)
[Node.js 中文网 — 如何安装 Node.js](https://nodejs.cn/en/learn/getting-started/how-to-install-nodejs)