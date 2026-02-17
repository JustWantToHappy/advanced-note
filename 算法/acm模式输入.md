# javascript
```javascript
const fs = require("fs")
const input = fs.readFileSync(0, 'utf-8').trim()

const data = input.split(/\s+/)
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