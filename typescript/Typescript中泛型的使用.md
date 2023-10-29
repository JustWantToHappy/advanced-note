## 定义
`泛型是指在函数，类，接口等定义中使用的一种抽象型，它可以在实际使用时被指定为具体的类型，从而增强代码的灵活性和重用性`
```typescript
function identity <T>(value: T) : T {
  return value;
}

//显式指定Number类型
console.log(identity<Number>(1)) // 1
//也可以不用指定类型，因为在编译阶段，编译器会自动确认类型
console.info(identity("sb"))

//定义多个类型变量
function identity <T, U>(value: T, message: U) : T {
  console.log(message);
  return value;
}

console.log(identity<Number, string>(68, "Semlinker"));

```
:::tips
这里解释一下上面实例中泛型的含义:<T>中的T表示定义了一个类型变量，在编译的过程中，后面的两个T表示的就是<T>被分配类型后传递过来的类型
:::
## 常见泛型变量

- K(Key):表示对象中键类型。
- V(Value):表示对象中的值的类型。
- E(Element):表示元素类型。
## 什么场景下使用泛型?

- 函数和类需要处理多种类型的数据，例如：当我们编写一个排序函数时，可能需要支持多种不同类型的数据进行排序。
- 提高代码的类型安全性，我们可以在编译时捕获错误，避免在运行时候出现类型相关错误。
## 为什么要使用泛型，为什么不能直接使用any？

- 缺乏类型安全性，使用any类型会导致ts缺乏对变量的类型检查，因此可能会在运行时发生类型错误，这些错误可能难以调试，并且可能导致应用程序崩溃。
- 代码可读性差，使用any类型就意味着你没有告诉其他开发人员变量应该期望哪种类型的数据。
- 难以维护，使用any类型会导致代码难以维护，当你使用any类型的变量传递给一个函数时，你无法确定函数的输入和输出类型，这可能会导致出现错误。
## 泛型接口
```typescript
interface Identites<K,V>{
    key: K;
    value:V
}
```
## 泛型类
```typescript
interface MyIdentity<K,V>{ 
    name: K;
    say: () => V;
}
export class Identity<T,P> implements MyIdentity<T,P>{
    name: T;
    say;
    constructor(name:T,hhh:P) {
        this.name = name;
        this.say = ()=>hhh;
    }
}
new Identity(1,false)
```
`解释一下：当我实例化Identity对象的时候，编译过程中，1和false的类型被编译为Number和Boolean,然后赋值给<T,P>，而Identity类实现了MyIdentity<T,P>接口，等价于该类实现了MyIdentity<Number,Boolean>接口`
## 泛型约束
作用:限制每个类型变量可以接受的类型数量。
### 确保属性存在
```typescript
interface identity{
    length: number;
}
export function Identity<T extends identity>(value:T) {
    console.info(value.length);
}
Identity("dsfsdfsdf");
Identity([1,2,2])


```
### 检查对象上的键是否存在
**首先了解一下keyof操作符的作用：用于获取某种类型的所有的键，其返回类型是联合类型**
```typescript
interface Real{
    name?: string;
    age?: number;
    bar: Function;
}
export function Bar<T, K extends keyof T>(obj: T,key:K):T[K] {
    return obj[key];
}
const obj:Real = {
    bar() { }
}
Bar(obj,'age');
/**
*错误实例:Bar(obj,'hh'),obj中没有类型hhh,报错
/
```
## 泛型参数默认参数
```typescript
interface identity<T = string>{
    name: T;
}


const a:identity={name:"sb"}

const b: identity <Number>= { name: 325 };
/**
错误实例:const c:identity={name:343}
*/
```
## 泛型条件类型
`T extends U? X : Y `
以上表达式的意思就是：若T能够赋值给U，那么类型是X，否则就是Y
`infer关键字的作用：提取一个函数类型的返回值类型`
```typescript
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;
//解释一下:(...args:any[])=>infer R表示的是这个函数不知道
返回值类型，使用infer让R称为这个函数的隐式返回值类型
如果T extends这个函数，那么类型ReturnType就是R，否则就是any
```
## 使用泛型创建对象
这里待写。。。有点消化不了
### 构造签名
