## 对象属性的遍历顺序不一定就是属性的书写顺序
```javascript
var obj={
    p2:'aaa',
    2:'aaa',
    1:'aaa',
    p1:'aaa'
}
for(const key in obj){
    console.log(key)
}
//1 2 p2 p1
```
遍历对象时，js会将key是数字属性的提前，对于提前的数字属性，再进行升序排序，字符串的属性按照你书写的顺序
### 为什么要这样做?
为了提高运行效率，对数字进行升序，是为了方便定位内存
