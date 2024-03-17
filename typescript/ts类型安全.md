## 类型安全
保证所有成员可用
## 父子类型
简单的父子类型
```typescript
interface Animal{
    name:string
}

interface Dog extends Animal{
    bark():viod;
}
```
- 在类型系统中，属性更多的类型是子类型。
- 在集合论中，属性更少的集合是子集(比如ts中的联合类型)。
```typescript
type Parent="a"|"b"|"c"
type Child="a"|"b"
let a:Parent;
let b:Child;
//兼容
a=b;
//不兼容，因为"c"不可能赋值给"a"|"b"
b=a;
```

### extends
> extends 是一个条件类型关键字，下面的代码可以这样理解，如果T是U的子类型，那么结果是X，否则类型就是Y
```typescript
T extends U? X:Y
```
当T是联和类型的时候，叫做分布式条件类型，类似于数学中的因式分解，举例：
```typescript
type Diff<T,U>=T extends U?never:T;

let demo:Diff<"a"|"b"|"d","d"|"f">
对于 Diff<"a", "d" | "f">，因为 "a" 不在 "d" | "f" 中，所以结果为 "a"。
对于 Diff<"b", "d" | "f">，因为 "b" 不在 "d" | "f" 中，所以结果为 "b"。
对于 Diff<"d", "d" | "f">，因为 "d" 在 "d" | "f" 中，所以结果为 never
//result:"a"|"b"
```
## 协变和逆变
- **协变**:允许子类型转换为父类型
- **逆变**:允许父类型转换为子类型

```typescript
let animal:Animal={age:12}
let dog:Dog={
    age:23,
    bark(){}
}
//兼容，能够赋值成功，这是一个协变
animal=dog;
//不兼容,缺乏属性bark
dog=animal
```
### 逆变
```typescript
interface Animal {
	age: number;
}

interface Dog extends Animal {
	bark(): void;
}
let animalFn = function (animal: Animal): Dog {
	return {
		age: 12,
		bark() { }
	}
}

let dogFn = function (dog: Dog): Animal {
	return { age: 2 }
}
//兼容
dogFn = animalFn
//不兼容
animalFn=dogFn
```

### 双向协变
在老版本的ts中，函数参数是双向协变的，也就是可以协变也可以逆变，在线版本的ts中，你可以通过开启strictFunctionTypes和strict来修复这个问题
