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
