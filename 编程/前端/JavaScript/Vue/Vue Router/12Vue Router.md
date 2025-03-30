---
aliases:
  - Vue
date: 2025-03-18
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

# 概念

- **路由配置**：定义了路径与组件之间的映射关系。
- **`<router-view>`**：一个用于渲染匹配到的组件的占位符。
- **`<router-link>`**：一个用于导航的自定义元素，类似于 HTML 中的 `<a>` 标签，但更适用于 SPA。

## 路由配置

## route-link

## route-view

# export

它的主要作用是将配置好的路由实例导出，使得其他文件可以通过import语句引入这个路由实例，并将其集成到Vue应用中。

# 教训

注意英语拼写，注意拼写，注意拼写！

这个异常 `main.js:7 [Vue Router warn]: No match found for location with path "/home"` 看了一晚上，横竖看不出来什么问题，就是报错，路由与路径不匹配

```js
import { createWebHistory, createRouter } from "vue-router";

// import HomeView from '../views/HomeView.vue'

import Home from '../components/Home.vue'

import About from '../components/About.vue'

import NotFound from '../views/404.vue'

// import Test from '../views/01.vue'

const routes = [

    { path: '/home', componet: Home },

    { path: '/about', componet: About},

    // { path: '/home', component: Home },

    // { path: '/about', component: About },

]
  
const router = createRouter({

    history: createWebHistory(),

    routes,

})

export default router
```

拼错了也不报错，也真是够离谱的！！！

![](教训.png)

# 配置路径别名

# 路由参数


# 参考资料

> [!note]
> [入门 | Vue Router](https://router.vuejs.org/zh/guide/)
