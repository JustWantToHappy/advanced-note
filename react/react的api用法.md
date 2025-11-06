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

## React.Children的方法
- React.Children.map方法
```tsx
const P = ({ children }) => {
	return (
		<div>
			{React.Children.map(children, (child, index) => {
				return (
					<h1>
						{child}
						{index}
					</h1>
				);
			})}
		</div>
	);
};

//使用
<P>
<>zzzz</>
<>hhhh</>
</P>

//UI展示结果：
zzzz1
hhhh1
```
- React.Children.count方法：获取当前组件的子节点的个数
- React.Children.toArray方法：将当前组件的子组件转换为数组
```tsx
const P = ({ children }) => {
	console.log(React.Children.toArray(children), children);
	return <></>;
};

//使用:
<P>
//当P的子组件只有一个的时候，上述打印结果分别是数组和一个对象，当子组件是多个的时候，打印结果都是数组
<>zzz</>
</P>

```
## 组件的key
```jsx
function ListItem(props) {
  //console.log(props.key);打印结果为undefined
  // 正确！这里不需要指定 key：
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // 正确！key 应该在数组的上下文中被指定
    <ListItem key={number.toString()} value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

注意，给组件设置过key之后，其下子元素无需再设置
