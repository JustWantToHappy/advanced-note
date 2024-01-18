## ToPrimitive操作
1. 如果obj是基本类型，直接返回
2. 否则，调用valueOf方法，如果得到原始值，则返回
3. 否则，调用toString方法，如果得到原始值，则返回
4. 否则，报错
## 类型转换
JS没有严格的数据类型，所以可以互相转换
- 显示类型转换：`Number()`,`String()`,`Boolean()`
- 隐式类型转换:四则运算，判断语句，`Native`调用，`JSON`方法
###　显式转换
1. Number()
```javascript
console.log(Number(1)) // 1
console.log(Number("1")) // 1
console.log(Number("1a")) // NaN
console.log(Number(true)) // 1
console.log(Number(undefined)) // NaN
console.log(Number(null)) // 0
console.log(Number({a:1})) // NaN
```
---
1. 先调用对象自身的valueOf方法,如果该方法返回原始类型的值，则直接对该值使用Number方法，不再继续.
2. 如果valueOf方法返回复合类型(引用类型)的值,再调用对象自身的toStirng方法，如果toString方法返回的是原始类型的值，则对该值使用Number方法，不再继续
3. 如果toString方法返回的还是复合类型的值，则报错
```javascript
//栗子
let obj={
    valueOf(){
        return {};
    },
    toString(){
        return {}
    }
}
```
2. String()
```javascript
console.log(String(1)) // "1"
console.log(String("1")) // "1"
console.log(String(true)) // "true"
console.log(String(undefined)) // "undefined"
console.log(String(null)) // "null"
console.log(String({b:1})) // "[object Object]"
```
- 先调用toString方法，如果toString方法返回的是原始类型的值，则对该值使用String方法，不再继续
- 如果toString方法返回的是复合类型，再调用valueOf方法，如果valueOf方法返回的是原始类型的值，则对该值使用String方法，不再继续
- 如果valueOf方法返回的是复合类型，则报错
3. Boolean()
- 0
- +0
- -0
- false
- ""
- null
- undefined
- NaN
以上统一转换为false，其他一律为true
### 隐式转换
```javascript
// 四则运算  如把String隐式转换成Number
console.log(+'1' === 1) // true

// 判断语句  如把String隐式转为Boolean
if ('1') console.log(true) // true

// Native调用  如把Object隐式转为String
alert({a:1}) // "[object Object]"
console.log(([][[]]+[])[+!![]]+([]+{})[!+[]+!![]]) // "nb"

// JSON方法 如把String隐式转为Object
console.log(JSON.parse("{a:1}")) // {a:1}

```
#### ==的隐式转换规则
1. 类型相同的比较
    1. 如果类型是Undefined或者Null,返回true
    ```javascript
    null==null//true
    ```
    2. 如果一个是+0，另一个是-0，返回true
    3. 如果类型都是对象，二者引用的是同一个对象，返回true,反之返回false
    ```javascript
    {}=={}//false
    ```
2. null和undefined的比较
```javascript
null==undefined//true
```
3. NaN比较：NaN与任何值比较都是false,包括自己
```javascript
NaN==NaN //false
```
4. 字符串与数字进行比较：如果其中一个操作符是字符串，另一个是数字，先将字符串转换为数字，然后进行比较
5. 布尔值与非布尔值进行比较：布尔值无法直接进行比较，需要先将布尔值转换为数字(true转换为1,false转换为0),非布尔值也需要转换为数字
```javascript
true=="1"//true
```
6. 对象与原始类型进行比较：如果其中一个是对象，另一个是原始类型，将对象通过`ToPrimitive`操作转换为原始类型，然后进行比较。（即如果原始类型为字符串，则对象转换成字符串再比较；如果原始类为布尔值，则将布尔值与对象都转换成数字进行比较；如果原始类为数字，则将对象转换成数字进行比较。）
```javascript
//例子
const a={
    n:1,
    valueOf(){
        return this.n++;
    }
}
console.info(a==1&&a==2&&a==3)//true
```