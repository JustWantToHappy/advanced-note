## any
当我们将某个变量定义成为any类型的时候，typescript会将会跳过对这个变量的类型检查。如果any类型的变量的属性，它的类型也会是any,因为any具有传递性
- 其他类型可以赋值给any
- any类型可以赋值给其他类型
## unknow
可以理解为类型安全的any，没有any的属性的类型传递性
```typescript
const a:unknown={name:"sb"}

const b=a?.name;//报错
```
- 任何类型可以赋值给unknow
- unknown类型的对象不可以直接赋值给其它非unknown或any类型的对象，并且不可以访问上面的任何属性
## never
...
## void
其实可以理解为null和undefined的联合类型
