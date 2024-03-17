## npm install

在本地 node_modules 文件夹中安装依赖项。

在全局模式下（即，将 `-g` 或 `--global` 附加到命令中），它将当前包上下文（即当前工作目录）安装为全局包。

默认情况下，`npm install` 将安装 [`package.json`](https://nodejs.cn/npm/cli/v6/commands/npm-install/##8f47a3c27ce24f8ba12683bc8c450434) 中列为依赖项的所有模块。

使用 `--production` 标志（或者当 `NODE_ENV` 环境变量设置为 `production` 时），npm 将不会安装 `devDependencies` 中列出的模块。当 `NODE_ENV` 环境变量设置为 `production` 时，要安装 `dependencies` 和 `devDependencies` 中列出的所有模块，您可以使用 `--production=false`。

> 注意：在向项目添加依赖项时，`--production` 标志没有特殊含义。

[npm 超详细教程 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/258080852)

[前端开发者需要知道的 package.json - 掘金 (juejin.cn)](https://juejin.cn/post/6969454249411837965)