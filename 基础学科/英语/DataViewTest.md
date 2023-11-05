
```dataview
list 
from #英语-词-名词 
```

测试 table

```dataview
TABLE file.cday, file.mtime FROM #英语-词-名词 
```

```dataviewjs 
const term = "get"

const files = app.vault.getMarkdownFiles()

const arr = files.map(async ( file) => {

const content = await app.vault.cachedRead(file)

const lines = content.split("\n").filter(line => line.contains(term))

return lines

})

Promise.all(arr).then(values =>

dv.list(values.flat()))
```

