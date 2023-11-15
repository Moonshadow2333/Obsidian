
```dataviewjs
let tagName = '#'+dv.current().file.name;
// tagName = "#英语-词-名词";
let text = '汇总标签'+tagName+'所有的数据：';
dv.paragraph(text);
dv.list(dv.pages(tagName).map(p => p.file.lists.text.filter(p => p.contains(tagName))))
```