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
## 动态集合问题
```javascript
var list=document.getElementById("list");
var listItems=document.getElementsByClassName("listItem");
var btn=document.getElementsByTagName("button")[0];
btn.onclick=function(){
    for(var i=0;i<listItems.length;i++){
        var cloned=listItems[i].cloneNode(true);
        //这样会出现问题，因为每次新增一个子元素，listItems元素集合就会变多，最后陷入死循环
        list.appendChildren(cloned);
    }
}
```
### 如何解决动态集合问题?
h5中新增的API:documet.querySelectorAll()方法获取静态集合

## 错误创建数组方式
```javascript
const arr = new Array(100).fill([]);
arr[0].push(1);
console.log(arr);//100个[1]
```
这样会导致所有数组元素都引用同一个对象地址，所以修改arr[0],其中就是修改同一个对象的属性，而arr[0]=1不会影响其他元素的原因是，将arr[0]的引用地址直接改成值了

## try-catch坑
- try-catch不能够捕获异步错误，例如:
```javascript
function asyncOperation() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      try {
        throw new Error("Error inside promise");
      } catch (err) {
        // This won't be reached
        console.error("Caught error inside promise:", err); 
      }
      resolve("Success");
    }, 1000);
  });
}
```