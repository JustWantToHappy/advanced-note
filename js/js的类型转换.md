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
- 先调用对象自身的valueOf方法,如果该方法返回原始类型的值，则直接对该值使用Number方法，不再继续.
- 如果valueOf方法返回复合类型(引用类型)的值,再调用对象自身的toStirng方法，如果toString方法返回的是原始类型的值，则对该值使用Number方法，不再继续
- 如果toString方法返回的还是复合类型的值，则报错
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
- 特殊情况
    - undefined==null
    - NaN!=NaN
- 类型相同:比较值
- 类型不同
    - 均为原始值：转换为数字比较
    - 一端为原始值，一端为对象：先调用valueOf，若无法转换为原始值，再调用toString
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