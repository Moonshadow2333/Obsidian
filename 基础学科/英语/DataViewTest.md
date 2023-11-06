
```dataviewjs 
const term = "#英语-词-动词"

const files = app.vault.getMarkdownFiles()

const arr = files.map(async ( file) => {

const content = await app.vault.cachedRead(file)

const lines = content.split("\n").filter(line => line.contains(term))

return lines

})

Promise.all(arr).then(values =>

dv.list(values.flat()))
```
