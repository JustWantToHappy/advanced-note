## 错误创建数组方式
```javascript
const arr = new Array(100).fill([]);
arr[0].push(1);
console.log(arr);//100个[1]
```
这样会导致所有数组元素都引用同一个对象地址，所以修改arr[0],其中就是修改同一个对象的属性，而arr[0]=1不会影响其他元素的原因是，将arr[0]的引用地址直接改成值了