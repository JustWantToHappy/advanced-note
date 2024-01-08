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
