# javascript
```javascript
const fs = require("fs")
const input = fs.readFileSync(0, 'utf-8').trim()

const data = input.split(/\s+/)
```
读到EOF（文件结尾）为止的多行输入
```javascript
const fs = require("fs")

const input = fs.readFileSync(0, "utf-8").trim().split("\n")

for (const line of input) {
  const s = line.trim()
  if (!s) continue
  console.log(s)
}
```
# python3
多个输入
```python
 n, m = map(int, input().split())
grid = []

# 也可以使用列表推导项输入：grid = [list(map(int, input().split())) for _ in range(n)]

for _ in range(n):
    row = list(map(int, input().split()))
    grid.append(row)

def main():
    print(grid)

if __name__=="__main__":
    main();

```
单个输入
```python
n=int(input())
```
读到EOF（文件结尾）为止的多行输入

第一种方式
```python
import sys
for line in sys.stdin:
    s = line.strip()
```
第二种方式
```python
while True:
    try:
        s = input()
        print(s)
    except:
        break
```