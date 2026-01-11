## Signals的定义
下一代状态管理方案，通过消息发布订阅的模式实现细粒度的精准更新，无需虚拟DOM进行diff(在状态层已经建立了“数据 → DOM”的精确依赖关系，更新时直接命中目标，不需要再做 diff 推断),类似的框架有solidjs等

## solidjs状态变更理解
```jsx

import { createEffect, createSignal } from "solid-js";

export default () => {
	const [count,setCount] = createSignal(0);

	console.log(count,'hhh');//打印只会执行一次
	
	createEffect(()=>{
		//这里会自动收集依赖 count，当 count 变化时，effect 会重新执行，比react智能很多
		if(count()>1){
			console.log('effect');
		}
	})

  return <h2>Child component<br/>
		<button onClick={()=>setCount(count=>count+1)}>{count()}</button>
	</h2>;
};

```