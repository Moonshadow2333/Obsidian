---
aliases:
  - CSS
  - animation
  - 动画
date: 2025-03-30
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

#  CSS 动画定义

用于实现元素从一个 CSS 样式配置转换到另外一个 CSS 样式配置

# 

#  animation-fill-mode

CSS 动画是网页设计中常用的一种元素交互效果，但有时候我们希望动画结束后元素能够保持在最后的位置而不是返回到原始位置。下面将介绍几种方法来实现这一点。

CSS提供了一个非常简单的方法来阻止动画返回到原始位置，即使用 `animation-fill-mode` 属性。该属性可以在动画结束后，将元素保留在动画的最后一个关键帧上。`animation-fill-mode` 属性可以设置以下几个值：

- `none`: 动画结束后，元素会立即返回到初始位置。这是默认值。
- `forwards`: 动画结束后，元素会停留在动画的最后一个关键帧上。
- `backwards`: 元素在动画开始之前将应用第一个关键帧中的样式。这意味着在动画开始之前元素会先呈现最后一个关键帧的样式。
- `both`: 结合了 `forwards` 和 `backwards` 的效果，即元素在动画结束后停留在最后一个关键帧上，并在动画开始之前呈现第一个关键帧的样式。

[animation-fill-mode - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-fill-mode)
[animation-fill-mode - CSS: Cascading Style Sheets | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-fill-mode#formal_definition)

# 参考资料

> [!note]
> - [javascript - 深入浅出 CSS 动画 - iCSS - SegmentFault 思否](https://segmentfault.com/a/1190000041275359)
> - [css3 - 如何理解animation-fill-mode及其使用？ - SegmentFault 思否](https://segmentfault.com/q/1010000003867335)