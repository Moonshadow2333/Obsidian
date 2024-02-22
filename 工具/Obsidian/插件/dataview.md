
```dataview
list 
from #英语-词-名词 
```

测试 table

```dataview
TABLE file.cday, file.mtime FROM #英语-词-名词 
```

```dataviewjs
dv.pages("#英语-词-动词");
dv.header(1, "Big!");
dv.header(6, "Tiny");
dv.paragraph("This is some text");
```

## 渲染

### 列表

列表 1,2,3

```dataviewjs
dv.list([1, 2, 3]);
```

库中所有文件名的列表

```dataviewjs
dv.list(dv.pages().file.name)
```

库中所有笔记链接的列表

```dataviewjs
dv.list(dv.pages().file.link)
```

测试

```dataviewjs
dv.list(dv.pages("#英语-非谓-动词ing").map(p => p.file.lists.text.find(p => p.contains("英语-非谓-动词ing"))))
```

#### map

对于所有元素执行相同操作  
如 `[1,2,3].map(p=>p+1)` 可以得到 `[2,3,4]`，这个 p 代指操作时的每一个元素，`p=>p+1` 本质上是个函数  
再比如 ``dv.pages(`"目标文件夹"`).map(p=>p.file.tags)`` 得到目标文件夹下所有笔记的标签

#### [](https://forum-zh.obsidian.md/t/topic/6627#filter-4)filter

只保留返回为 true 的元素  
如 ``dv.pages(`"目标文件夹"`).filter(p=>p.file.tags.includes('标签')`` 只保留了标签中含 `标签` 的那些文件数据

#### [](https://forum-zh.obsidian.md/t/topic/6627#array-5)Array