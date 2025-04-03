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

# 两步实现动画

实现 CSS 动画需要两个步骤：

1. 第一步——描述规则：描述动画的样式规则
2. 第二步——指定关键帧：指定动画开始、结束以及中间样式的关键帧

例子：

```css
div {
	// 第一步，描述动画的规则
    animation: change 3s;
}

// 第二步，指定关键帧
@keyframes change {
    0% {
        color: #f00;
    }
    100% {
        color: #000;
    }
}
```

# CSS 动画语法

> 创建动画序列，需要使用 animation 属性或其子属性，该属性允许配置动画时间、时长以及其他动画细节，但该属性不能配置动画的实际表现，动画的实际表现是由 @keyframes 规则实现。

```css
.ele {
	animation: animation-name animation-duration;
}

@keyframes animation-name{
	设定动画关键帧...
}
```

animation 子属性：

| 序号 | 子属性                    | 功能                                                                |
| ---- | ------------------------- | ------------------------------------------------------------------- |
| 1    | animation-name            | 指定由 @keyframes 描述的关键帧名称                                  |
| 2    | animation-duration        | 设置动画一个周期的时长                                              |
| 3    | animation-delay           | 设置延时，即从元素加载完成之后到动画序列开始执行的这段时间          |
| 4    | animation-direction       | 设置动画在每次运行完后是反向运行还是重新回到开始位置重复运行        |
| 5    | animation-iteration-count | 设置动画重复次数， 可以指定 infinite 无限次重复动画                 |
| 6    | animation-play-state      | 允许暂停和恢复动画                                                  |
| 7    | animation-timing-function | 设置动画速度， 即通过建立加速度曲线，设置动画在关键帧之间是如何变化 |
| 8    | animation-fill-mode       | 指定动画执行前后如何为目标元素应用样式                              |
| 9    | @keyframes 规则           | 在内部设定动画关键帧                                                | 

必须项：animation-name、animation-duration 和 @keyframes规则
非必须项：animation-delay、animation-direction、animation-iteration-count、animation-play-state、animation-timing-function、animation-fill-mode，当然不是说它们不重要，只是不设置时，它们都有默认值

##  animation-fill-mode

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