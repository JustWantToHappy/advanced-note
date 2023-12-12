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