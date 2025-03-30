---
aliases:
  - Vue
  - 入门
  - 安装
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

# 安装 Vue

```
npm install vue
npm install vue-router
```

# 打包工具选择

[一篇文章说清 webpack、vite、vue-cli、create-vue 的区别 - 知乎](https://zhuanlan.zhihu.com/p/511524474)
[Vite和Vue Cli对比Vite与Vue Cli Vite和Vue Cli可以是师出同门，功能都类似，他们之间到底什 - 掘金](https://juejin.cn/post/7018754950498877471)

## Vite

[开始 | Vite 官方中文文档](https://vitejs.cn/vite3-cn/guide/#trying-vite-online)