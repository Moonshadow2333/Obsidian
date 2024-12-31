---
aliases:
  - 属性绑定
date: 2024-12-29
---

# v-bind

为了给 attribute 绑定一个动态值，需要使用 v-bind 指令：

```
<div v-bind:id="dynamicId"></div>
```

- 指令是由 v- 开头的一种特殊 attribute。它们是 Vue 模板语法的一部分。
- 和文本插值类似，指令的值是可以访问组件状态的 JavaScript 表达式。
- 冒号后面的部分 (`:id`) 是指令的“参数”。此处，元素的 `id` attribute 将与组件状态里的 `dynamicId` 属性保持同步
- 由于 `v-bind` 使用地非常频繁，它有一个专门的简写语法：`<div :id="dynamicId"></div>`

# 代码

```js
<script setup>
import { ref } from 'vue'

const titleClass = ref('title')
</script>

<template>
  <h1 :class="titleClass">Make me red</h1>
</template>

<style>
.title {
  color: red;
}
</style>
```