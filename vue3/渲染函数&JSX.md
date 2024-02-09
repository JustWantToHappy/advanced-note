## 创建Vnodes
vue提供了一个`h()`函数用于创建vnodes,h函数实现了函数重载，提供了多种参数形式
```typescript
import { h } from 'vue'

const vnode = h(
  'div', // type
  { id: 'foo', class: 'bar' }, // props
  [
    /* children */
  ]
)
```
## 声明渲染函数
```typescript
import { ref, h, defineComponent } from "vue";

export default defineComponent({
	props: {
		message: String,
	},
	setup(props) {
		const count = ref(0);

		return () => h("div", count.value + props.message);
	},
});

```
除了返回一个vnode，你还可以返回一个字符串或者数组
```typescript
export default {
  setup() {
    return () => 'hello world!'
  }
}
```
```typescript
import { h } from 'vue'

export default {
  setup() {
    // 使用数组返回多个根节点
    return () => [
      h('div'),
      h('div'),
      h('div')
    ]
  }
}
```
## vnode必须唯一
下面是错误示范
```typescript
function render() {
  const p = h('p', 'hi')
  return h('div', [
    // 啊哦，重复的 vnodes 是无效的
    p,
    p
  ])
}
```
如果你真的非常想在页面上渲染多个重复的元素或者组件，你可以使用一个工厂函数来做这件事。比如下面的这个渲染函数就可以完美渲染出 20 个相同的段落
```typescript
function render() {
  return h(
    'div',
    Array.from({ length: 20 }).map(() => {
      return h('p', 'hi')
    })
  )
}
```

## jsx写法
```typescript
//Demo.tsx

import {
	FunctionalComponent as FC,
	defineComponent,
	ref,
	onMounted,
} from "vue";
import style from "@/less/Demo.module.less";
//无状态组件
export const FcNode: FC<{ name: string }> = (props) => {
	console.log(props.name);
	return (
		<>
			<h1 class="sb">zzz</h1>
		</>
	);
};

//状态组件需要使用defineComponent
export default defineComponent({
	name: "Demo",
	setup() {
		const message = ref("hello world！");
		onMounted(() => {
			console.log("mounted");
		});
		return () => <div class={style.container}>{message.value}</div>;
	},
});

```

## 模板、渲染函数与jsx的栗子
- 模板语法
```html
<div>
  <div v-if="ok">yes</div>
  <span v-else>no</span>
</div>
```
- 渲染函数语法
```javascript
h('div', [ok.value ? h('div', 'yes') : h('span', 'no')])
```
- jsx语法
```jsx
<div>{ok.value ? <div>yes</div> : <span>no</span>}</div>
```