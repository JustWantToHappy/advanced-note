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