## 局部UI消费
- 重组件不需要消费Provider，父组件使用useContext导致值发生变化，重组件reRender，可以将中组件抽离出去，如使用{children}插槽给重组件占位
## useReducer+Provider的技巧

```tsx
import { Button } from "antd";
import { createContext, useContext, useReducer, useState } from "react";
//正确使用Provider姿势

const DataContext = createContext<{ data?: number[] }>({});

const DispatchDataContext = createContext<{
	dispatchData?: Function;
}>({});

const reducer = (state: number[], action: { type: "push" }) => {
	if (action.type === "push") {
		return [...state, Math.floor(Math.random() * 100)];
	}
	return state;
};

const RenderDispatchData = () => {
	const { dispatchData } = useContext(DispatchDataContext);
	return (
		<Button onClick={() => dispatchData?.({ type: "push" })}>Click</Button>
	);
};

const RenderData = () => {
	const { data } = useContext(DataContext);
	return <ul>{data?.map((item) => <li key={item}>{item}</li>)}</ul>;
};

const App = () => {
	const [data, dispatchData] = useReducer(reducer, []);

	return (
		//将 state 和 dispatch 分开传递，避免不必要的重渲染
		<DataContext.Provider value={{ data }}>
			{/* dispatch函数在App组件的整个生命周期中(挂载到卸载)，是一个引用不变的对象 */}
			<DispatchDataContext.Provider value={{ dispatchData }}>
				<RenderDispatchData />
			</DispatchDataContext.Provider>
			<RenderData />
		</DataContext.Provider>
	);
};

export default App;

```