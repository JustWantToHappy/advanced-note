## 联合类型和交叉类型的结果
```typescript
type A=string|number;
type B=string|null;
type C=A&B;//string;
```
## 索引类型查询
- key为字符串
```typescript
export interface ViewTableProps {
	onChange: () => void;
}

const sb: ViewTableProps["onChange"] = function () { }
```
- key为number,T[number]
```typescript
const tuple = ["tesla", "model 3", "model X", "model Y"] as const;

type TupleToObject<T extends readonly (string | symbol | number)[]> = {
	[P in T[number]]: P;
};
```
- 如果要访问指定的数字下标，可以使用T[0],T[1]...
- 如果泛型是个数组，可以通过T["length"]得到长度
```typescript
type Length<T extends unknown[]> = T["length"];
```
### 与索引类型签名的区别
索引类型签名用于描述对象中可以包含任意属性的方式,例如：
```
type Demo={
    [key:string]:string;
}
```
## 映射类型
ts许多内置类型中都使用了映射类型
```typescript
type Partial<T>={
	[P in keyof T]?:T[P]
}
type B={
	[P in string]:any;
}
```
## as const
as const是一种类型断言，它将一个表达式断言为不可变的常量
```typescript
//这里加上as const会使ts推断出更加具体的类型信息，不加上as const则是普通的string类型
const colors = ["red", "green", "blue"] as const;

type Color = (typeof colors)[number];//"red"|"green"|"blue"

```

## 重命名
```typescript
interface Student {
	id: string;
	name?: string;
	age?: number;
}

type RenameKeys<T> = {
	[P in keyof T as `get${P & string}`]: T[P];
};

const obj:RenameKeys<Student>
obj.getage;

```
## ts类型推断
```typescript
type UnionTest = ((x: { a: string }) => any) | ((x: { b: number }) => any);

function fn(cb: UnionTest) {
	cb({ a: "1", b: 1 });//这里推导出来的类型是{a:string}&{b:number}
}

```

