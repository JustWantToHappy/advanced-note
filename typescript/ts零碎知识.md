## 联合类型和交叉类型的结果
```typescript
type A=string|number;
type B=string|null;
type C=A&B;//string;
```