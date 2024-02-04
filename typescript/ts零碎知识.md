## 联合类型和交叉类型的结果
```typescript
type A=string|number;
type B=string|null;
type C=A&B;//string;
```
## 索引类型查询
```typescrpt
export interface ViewTableProps {
	onChange: () => void;
}

const sb: ViewTableProps["onChange"] = function () { }
```
### 与索引类型签名的区别
索引类型签名用于描述对象中可以包含任意属性的方式,例如：
```
type Demo={
    [key:string]:string;
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