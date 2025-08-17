---
aliases:
  - 数据库
date: 2025-06-15
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


# 算法：  

 INPUT：关系模式R 以及在R上成立的函数依赖集F  
 
1. 初始化 P = {R}  
2. 若P中的所有关系模式S都是BCNF，则转步骤（4）  
3. 若P中有一个模式S不是BCNF，则S中必能找到一个函数依赖X->A，X不是S的候选码，且A不属于X。设S1 =XA，S2 = S-A，分解后的{S1,S2}替代S，转步骤（2）  
4. 算法结束，输出P  

    *注：学习的前置条件：会求候选码  

    *注：步骤3中，A不属于X的含义： 如果有函数依赖 CD->C，则C是属于{CD}的，如果C->D,则D是不属于{C}的。  

    *注：模式S的解释：如P={R1（ABC），R2（KMG）}，这里的S可以指代R1，也可以指代R2。

    *注：如何判断BCNF：函数依赖项的左侧都是候选码，即为BCNF。  


# 例子  

例：R={A,B,C,D,E,F,G}，F={A—>B, A—>C ,C—>D, C—>E, E—>FG}，将R分解成BCNF。

解：

    步骤1：初始化P={R} = {R(A,B,C,D,E,F,G）}  

    步骤2：计算一下R的候选键，易知R的候选键为A。  

    步骤3-1：从函数依赖集F中容易发现，A—>B, A—>C 是满足BCNF的，C—>D不满足，且D不属于{C}，因此

    令S1 = CD，S2=S-{D} = {A,B,C,E,F,G}，替换R  

    即P={R1（C,D），R2（A,B,C,E,F,G）}。

    此时，F分成两部分。F1={C—>D}，F2={A—>B, A—>C , C—>E, E—>FG}

    步骤3-2：由R1已经满足BCNF了，所以不用管它了。继续计算R2的候选键，易知R2的候选键为A

    同样，A—>B, A—>C满足BCNF了，C—>E不满足，且E不属于{C}，因此

    令R3 = CE，R4 = R2-E={A,B,C,F,G}，替换R2。（为了书写美观，写加入后的R3写为R2，R4写为R3，后续同样操作，不再赘述）  

    即P={R1（C,D），R2（C,E），R3(A,B,C,F,G)}。

    此时，F2分成两部分，新的F3={C->E},F4={A—>B, A—>C , C—>FG}

    即：F1={C—>D}，F2={C->E},F3={A—>B, A—>C , C—>FG}

  

    *注：特别关注函数依赖C—>FG，是由C—>E, E—>FG导出的传递依赖。给与我们的提示是，在书写新的函数依赖集时，千万不要遗漏掉传递依赖等性质推出的新依赖。

  

    步骤3-3：由R1，R2已经满足BCNF了，所以不用管它了。继续计算R3的候选键，易知R3的候选键为A

    此时A—>B, A—>C 已经满足BCNF了，而C—>FG不满足，且C不属于{FG}

    因此令R4=CFG，R5=R3-{FG} = {A,B,C}。  

    因此替换掉原来的R3，即：  即P={R1（C,D），R2（C,E），R3(C,F,G)，R4(A,B,C）}。

    F3分解为两部分，F4={ C—>FG},F5={A—>B, A—>C}。

    即：F1={C—>D}，F2={C->E}，F3={ C—>FG}，F4={A—>B, A—>C}。

      

    显然，R4的候选键为A，且F4中的函数依赖左侧都是候选键，因此P中的所有分解都满足BCNF。故算法结束

    综上，分解为P={R1（C,D），R2（C,E），R3(C,F,G)，R4(A,B,C）}。

  
------------------------------------  
作者：程俊伟  
来源：学者网  
原文：https://www.scholat.com/vpost.html?pid=144469  
本文为该学者原创文章，转载请附上文章链接！

