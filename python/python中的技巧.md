## max,sum函数可以使用迭代器
```python
stack=[1,2,3]
sums=0
sums=sum(stack[i]+1 for i in range(3))
print(sums)
```
## 海象运算符
```python
if (diff:=a-b)>0:
    print(diff)
#比较的同时定义变量
```

## 解包运算符
```python
# grid是一个二维数组，比如row是[2,3,4]，如果加上*，则打印2 3 4，如果不加则打印[2,3,4]
for row in grid:
    print(*row)
```
