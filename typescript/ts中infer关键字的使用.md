- 解析包:
```
type Ids=Number[]


type Unpacked<T> = T extends (infer R)[] ? R : T;


type PromiseType=Promise<Promise<Number[]>>

type Unpacked1<T> = T extends Promise<Promise<infer R>[]> ? R : T;
```

- 推断模板字符串
```
type TrimLeft<T> = T extends ` ${infer R}` ? TrimLeft<R> : T;

type TrimRight<T> = T extends `${infer R} ` ? TrimRight<R> : T;

type b=TrimLeft<TrimRight<'   value   '>>
```

- 推断联合类型
```
//推断元组
type Tupple = [number, string, boolean?]

type InferTupple<T> = T extends (infer R)[] ? R : never;

type C=InferTupple<Tupple>

//推断对象类型
type Foo<T> = T extends { a: infer R, b: infer R } ? R : never;

type foo = Foo<{ a:string,b:number}>

```

- 遍历数组
```
type ReverseArray<T extends unknown[]> = T extends [infer First, ...infer Rest]  
? [...ReverseArray<Rest>, First]  
: T  
type Value = ReverseArray<[1, 2, 3, 4]> // [4,3,2,1]

```
