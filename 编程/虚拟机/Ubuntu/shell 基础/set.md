---
aliases:
  - set
  - 设定参数
  - 参数
  - Linux 命令
  - shell 指令
date: 2024-12-15
---

# 用法

set 命令为 shell 设定参数变量。许多命令的输出是以空格分隔的值，如果要使用其中的某个数据域，使用 set 非常有效。

```
#!/bin/sh  
echo the date is $(date)  
set $(date)  
echo the month is $2  
输出：  
the date is Wed Apr 23 15:34:16 CST 2014  
the month is Apr

将 date 命令的输出设置为参数表，再通过位置参数 $2 取得月份。
```

> [!note] 参考资料
> [Shell 中的set --用法 - 滴滴滴 - 博客园](https://www.cnblogs.com/gaoyuechen/p/14336063.html)
