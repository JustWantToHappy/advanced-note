## typeof
```typescript
interface Person{
    name: string;
    age: number;
}
const sem:Person={name:"sb",age:90}
type Sem = typeof sem;//interface Person{...}
let str="hhhh"
type demo=typeof str;//注意，此处不能使用typeof demo=typeof 'hhhh',这是因为typeof操作的必须是一个变量
```
## ?.
可选链操作符
```typescript
//ts
const val=a?.b
//es5
var val=a===null||a.b
//注意：其实es6中也有?.
```
也可以这样使用的：
```typescript
 interface Student{
        name: string;
        age: number;
    }
    let sb:Student={name:"shhh",age:1}
    sb?.['name']
```
## !(非空断言运算符)
用于断言操作的对象是非null和非undefined类型
```typescript
function test(callback: () => number | undefined) {
        const number = callback!();//除去undefined
    }
    let a: number | undefined | null;
    // let b: number = a;(这样写必然报错，因为类型不兼容)
    let b: number = a!;
```
## ?:
可选属性，主要用于类型声明的时候对某个属性进行标记，这样在实例化的时候缺少某个属性编译器就可以不报错
```typescript
interface Person{
    name : string;
    age : number;
    gender? : string // 可选属性
}
```
## 必选参数-?
```typescript
type Required<T>={
    [key in keyof T]-? : T[key] 
}
```
## ??(空值合并运算符号)
当左侧的值为null或者是undefined的时候，返回右侧的值，否则就返回左侧的值操作数
## &(交叉类型运算符)
可用于将多个类型叠加到一起形成一个新的类型
```typescript
//接口中使用
  interface DogInterface {
        run(): void;
    }
    interface CatInterface {
        jump(): void;
    }
    //pet就是一个交叉类型
    let pet: DogInterface & CatInterface = {
        run() { },
        jump() { }
    }
```
## |(联合类型运算符)
表示取值可以是多种类型中的一种
```typescript
  let a: number | undefined | null = 1;
    let b: number | undefined | null = undefined;
    let c: number | undefined | null = null;
```
## _（数字分割符)
不会改变字面量的值，用于逻辑分组便于阅读
```typescript
const number=2022_0101_0000;
//注意，es6中也有此用法
```
## #(私有字段，在class中使用)
它的作用类似private字段
```typescript
 class Student {
        #name: string;
        constructor(name: string) {
            this.#name = name;
        }
        getName() {
            return this.#name;
        }
    }
    var student = new Student('student');
    student.getName();//私有属性必须通过get方法获取
```
## in
作用：对联合类型进行遍历
```typescript
type Keys = "firstName" | "lastName";
type Person = {
  [key in Keys]: string;
}; // {firstName: string; lastName: string}
```
## extends
根据条件返回结果，类似三元运算符。
## infer
## readonly
## keyof
作用：获取对象或数组等类型的所有键，并返回一个联合类型
```typescript
interface Person {
  name: string
  age: number
}

type K1 = keyof Person  // "name" | "age"

type K2 = keyof []      // "length" | "toString" | "push" | "concat" | "join"

type K3 = keyof { [x: string]: Person }  // string | number
```