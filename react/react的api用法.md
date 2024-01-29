## forwardRef
- forwardRef用法
```jsx
 forwardRef(function MyInput(props, ref) {
  // ...
});
```
- forwardRef给接收的参数设置类型：
```tsx
forwardRef<refType,propsType>((props,ref)=>{})
```

## useImperativeHandle用法
```tsx
//该 ref 是你从 forwardRef 渲染函数 中获得的第二个参数。
React.useImperativeHandle(ref, () => ({
    //你要导出的属性...
}));
```
## createPortal
`createPortal`允许你将jsx作为children渲染到DOM的不同部分
```tsx
import {createPortal} from "react-dom"

// ...

<div>
  <p>这个子节点被放置在父节点 div 中。</p>
  {createPortal(
    <p>这个子节点被放置在 document body 中。</p>,
    document.body
  )}
</div>
```