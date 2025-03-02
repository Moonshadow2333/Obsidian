---
aliases:
  - 新概念
date: 2025-02-23
---

# 目录

```dataviewjs
const startHeadinglevel = 2;
const file = app.workspace.getActiveFile();
const { headings } = app.metadataCache.getFileCache(file);

// 全列表的形式
const raws = headings.map( p => {
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

# 课文注释

## while 作名词

while 作名词表示“一会儿“、”一段时间“，时常与 a 连用，有时也与 the，this 等连用

- a long while 很长时间
- all this while 这段时间
- a short while ago 刚才

## 用 far 表强调

在形容词和副词的比较级与最高级前面，可以用 far （相当于 much）来表示强调

- far more exciting 令人兴奋得多

## 感知动词的用法

- 感知动词：feel、hear、notice、smell、watch、see
- 感知动词可以用动词 + 名词或代词宾语 + 不带 to 的不定式结构中

例子：

I saw him climbed through the window. 我看见他爬进窗户

这些动词的**宾语相当于不定式的主语（him 相当于不定式 climbed through the window 的主语）**，上句即：

I saw that he climbed through the window

## with 表拿着

The one with the money got such a fright that he dropped the bag. 拿钱的哪个小偷吓得把提包都扔了。

## 分词作定语

### 现在分词

a waiting car, waiting 为现在分词作定语，表示”等待着的“、”等在那里的“

### 过去分词

the battered car，那辆被撞坏的车，battered 过去分词，作定语，相当于 the car which was battered

## 短语动词

### get away

逃跑、逃脱

How did the thief get way? 小偷是如何逃掉的？

### drive into

把汽车开进

Roy drove his bus into the back of it. 罗伊驾驶他的公交车撞在了那辆车的后尾上。

# 时态

## 一般现在时

通常用于表示目前的状态或动作以及习惯性的动作。

## 一般过去时

指过去某个时间所做的动作，不强调与现在的关系

used to 只能用于过去时，表示过去有过而现在已经没有的习惯

## 现在完成时

现在完成时通常指过去发生的但与现在有联系的动作

## 被动语态

# 词汇

## rush

- vi. 冲，奔
	- Two thieves rushed out of a shop. 两个小偷从一家商店里冲了出来
	- While I was talking to Frank, a man rushed into the room. 我和 Frank 谈话时，一个人冲进了房间
- vt.，vi. 仓促行事，仓促完成，赶紧做
	- Tom always rushes his homework on Sunday evenings. Tom 总是在星期天晚上赶做他的作业
- n. 猛冲，奔
	- Roy made a rush at the thieves. 罗伊冲向小偷们

## straight

- adj. 直的，笔直的
	- This road isn't straight. 这条路不直
- adv. 笔直地
	- He walked straight on. 他一直往前走
- adv. 经直地
	- John always goes straight home after work. John 下班后总是直接回家

## such so

- so 修饰形容词或副词
- such 修饰名词
- such a/an 修饰单数可数名词