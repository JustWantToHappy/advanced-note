## 自定义Equal泛型工具的bug
```typescript
type IsEqual<T, U> = T extends U ? (U extends T ? true : false) : false;

//为什么不是false?目前发现只有在联合类型判断时会有这个问题
type A = IsEqual<string, string | number>;//result:boolean

```