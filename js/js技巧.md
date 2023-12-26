## >>
使用>>除法取整，比如(1+4)>>1,等同于`Math.floor((1+4)/2)`

## +=
a+=b>c等同于
```javascript
if(b>c){
    a+=1
}
```
## 结束外层循环
标记语法
```javascript
outerloop: for (let i = 0; i < 10; i++) {
	for (let j = 0; j < 10; j++) {
		if (i + j > 10) {
			break outerloop
		}
	}
}
```
