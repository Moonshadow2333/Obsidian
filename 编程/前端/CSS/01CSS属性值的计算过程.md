---
aliases:
  - CSS
  - 属性值计算过程
  - 视觉格式化模型
date: 2025-03-23
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

# 属性值计算过程

![[CSS 属性计算过程简介]]

## 目标

了解某个元素从所有 CSS 属性没有值，到所有 CSS 属性都有值的过程

## 计算过程

1. 确定声明值
2. 解决层叠冲突
3. 继承
4. 使用默认值

### 确定声明值

将没有样式冲突的属性先确定下来

### 解决层叠冲突

即对样式表中有冲突的声明使用层叠规则，确定css属性值

#### 层叠规则

- 重要性：!important > 用户样式表 > 浏览器默认样式表
- 特殊性：行内样式、ID、类、元素的特殊性由高到低
	- 行内样式(`<p style=""></p>`)
	- ID 选择符的数目
	- 类选择符的数目
	- 类型（标签）选择符和伪元素选择符的数目
- 源次序：如果出现特殊性相等，则优先应用后定义的规则

### 继承

到了这一步尽管确定了一些没有冲突的，有冲突的属性值，但是还是有一些属性的值没有确定，因为有一些属性用户样式表和浏览器默认样式表中都没有进行声明。所以这一步，**对仍然没有值的属性，若可以继承**，则继承父元素的值

CSS 可以继承的属性：

```php
1.字体系列属性

font：组合字体

font-family：规定元素的字体系列

font-weight：设置字体的粗细

font-size：设置字体的尺寸

font-style：定义字体的风格

2、文本系列属性

text-indent：文本缩进

text-align：文本水平对齐

line-height：行高

word-spacing：增加或减少单词间的空白（即字间隔）

letter-spacing：增加或减少字符间的空白（字符间距）

text-transform：控制文本大小写

direction：规定文本的书写方向

color：文本颜色

3、元素可见性：visibility

4、表格布局属性：
caption-side、border-collapse、border-spacing、empty-cells、table-layout

5、列表属性：
list-style-type、list-style-image、list-style-position、list-style

6、光标属性：cursor
```

### 使用默认值

到了这一步，对仍然没有值的属性，使用默认值

## 例子

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        div {
            color: red;
        }
    </style>
</head>
<body>
       <div>
            <a href="">hello</a>
            <p>hi</p>
       </div> 
</body>
</html>
```

上述代码中：`a` 标签显示蓝色，`p` 标签显示红色

说明：

`div` 标签里套了一个 `a` 标签以及一个 `p` 标签，

```html
<div>
	<a href="">hello</a>
	<p>hi</p>
</div> 
```

给 `div` 设置的样式如下：

```css
div {
	color: red;
}
```

`div` 的样式是直接作用在 `div` 上面的，并没有给 `a` 和 `p` 标签直接设置样式，即 `a` 和 `p` 标签不存在样式冲突。

`a` 标签浏览器默认样式：

```css
a:-webkit-any-link {
    color: -webkit-link;
    cursor: pointer;
    text-decoration: underline;
}
```

可以看到 `a` 的浏览器默认样式中存在 `color` 属性，直接确认了声明值，也就是 `-webkit-link`。

`p` 标签浏览器的默认样式：

```css
p {
    display: block;
    margin-block-start: 1em;
    margin-block-end: 1em;
    margin-inline-start: 0px;
    margin-inline-end: 0px;
    unicode-bidi: isolate;
}
```

可以看到 `p` 标签浏览器默认样式中不存在 `color` 属性，接着看第二步，解决层叠冲突，这里没有冲突，所以看第三步，继承，文本颜色是可以继承的，所以会继承父元素 `div` 的颜色属性，也就是红色，到此结束。

## 问题

浏览器的默认样式和默认值有什么区别？

- 来源不同：浏览器的默认样式来自浏览器厂商预设的样式表，即用户代理样式表；而默认值是由W3C CSS规范定义的每个属性的初始值。
- 作用范围不同：浏览器默认样式影响的是特定HTML元素的整体外观（比如字体、颜色、边距等），而默认值是指单个CSS属性在没有任何声明时所具有的值。
- 可覆盖性：两者都可以被开发者通过自定义CSS覆盖，但是覆盖浏览器的默认样式通常涉及更广泛的样式调整，而设置或重置CSS属性的默认值则更加具体和直接。

# 视觉化格式模型

# 参考资料

- [聊聊css属性值的计算过程 - 简书](https://www.jianshu.com/p/2b88de19d3f7)