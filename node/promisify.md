## Node风格的回调
nodejs中大量API都是这样使用的
```javascript
fs.readFile('a.txt', 'utf8', (err, data) => {
  if (err) return console.error(err)
  console.log(data)
})

```
## promisify
utils.promisify就是将这种风格转换为async-await风格的工具
```javascript
const utils=require("utils");
const readFile = util.promisify(fs.readFile)

async function run() {
  const data = await readFile('a.txt', 'utf8')
  console.log(data)
}


```