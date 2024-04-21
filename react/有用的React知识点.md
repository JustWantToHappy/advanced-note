## 设置默认属性
```tsx
const About: React.FC<{ style?: React.CSSProperties }> = ({ style }) => {
	return <p style={style}>About</p>;
};
About.defaultProps = {
	style: {
		color: "orange",
	},
};

function App() {
	return (
		<div className="App">
			<About />
		</div>
	);
}
```
## 返回一个数组
```tsx
const Demo = () => {
	return [<div>1</div>, <div>2</div>];
};
```
```tsx
const App=()=><Demo/>
```