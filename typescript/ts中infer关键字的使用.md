- 解析包:
```typescript
type Ids=Number[]


type Unpacked<T> = T extends (infer R)[] ? R : T;


type PromiseType=Promise<Promise<Number[]>>

type Unpacked1<T> = T extends Promise<Promise<infer R>[]> ? R : T;
```

- 推断模板字符串
```typescript
type TrimLeft<T> = T extends ` ${infer R}` ? TrimLeft<R> : T;

type TrimRight<T> = T extends `${infer R} ` ? TrimRight<R> : T;

type b=TrimLeft<TrimRight<'   value   '>>
```

- 推断联合类型
```typescript
//推断元组
type Tupple = [number, string, boolean?]

type InferTupple<T> = T extends (infer R)[] ? R : never;

type C=InferTupple<Tupple>

//推断对象类型
type Foo<T> = T extends { a: infer R, b: infer R } ? R : never;

type foo = Foo<{ a:string,b:number}>

```

- 遍历数组
```typescript
type ReverseArray<T extends unknown[]> = T extends [infer First, ...infer Rest]  
? [...ReverseArray<Rest>, First]  
: T  
type Value = ReverseArray<[1, 2, 3, 4]> // [4,3,2,1]

```
- 函数柯里化<br>
每次只能够传递1个参数或者不传递参数的情况：
```typescript
type Curried<A, R> = A extends []
	? () => R
	: A extends [infer B]
	? (params: B) => R
	: A extends [infer B, ...infer Rest]
	? (params: B) => Curried<Rest, R>
	: never;

declare function curry<A extends any[], R>(
	fn: (...args: A) => R,
): Curried<A, R>;

//A extends []的情况
function sum() {}

const a = curry(sum); //()=>void;

//A extends [params:B]的情况
function sum(a: number) {
	return ''
}

const a = curry(sum); //(params:number)=>string;

//A extends [infer B,...infer Rest]的情况
function sum(a: number,b:number) {
	return ''
}

const a = curry(sum); //(params:number)=>(params:number)=>string;
```