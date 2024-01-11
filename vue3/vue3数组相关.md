## 变更方法
Vue 能够侦听响应式数组的变更方法，并在它们被调用时触发相关的更新。这些变更方法包括：
- push()
- pop()
- shift()
- unshift()
- splice()
- sort()
- reverse()
## v-for指令
使用v-for指令基于一个数组来渲染一个列表，必须给列表项添加key属性
```html
<script lang='ts' setup>
import { ref } from "vue"
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
</script>

<template>
	<ul>
        //这里也可以使用v-for="item of items"代替
		<li v-for="item in items" :key="item.message">
			{{ item.message }}
		</li>
	</ul>
</template>
<style lang="less" scoped></style>
```
对于多层嵌套的 v-for，作用域的工作方式和函数的作用域很类似。每个 v-for 作用域都可以访问到父级作用域：
```html
<li v-for="item in items">
  <span v-for="childItem in item.children">
    {{ item.message }} {{ childItem }}
  </span>
</li>
```
## v-for与对象
```html
<script lang='ts' setup>
import { ref, reactive } from "vue"
const myObject = reactive({
	title: 'How to do lists in Vue',
	author: 'Jane Doe',
	publishedAt: '2016-04-10'
})
</script>

<template>
	<ul>
        //例如：0 title "How to do lists in Vue" 分别对应index key value
		<li v-for="(value, key, index) in myObject" :key="key">
			{{ index }}. {{ key }}: {{ value }}
		</li>
	</ul>
</template>
```
## 在v-for里面使用范围值
```html
<span v-for="n in 10">{{ n }}</span>
```
注意此处 n 的初值是从 1 开始而非 0。
## <template>上的v-for
## v-if和v-for
同时使用v-if和v-for是不推荐的,当它们同时出现在同一个节点上的时候，v-if 比 v-for 的优先级更高。这意味着 v-if 的条件将无法访问到 v-for 作用域内定义的变量别名
- 不推荐写法
```html
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo.name }}
</li>
```

- 推荐写法
```html
<template v-for="todo in todos">
  <li v-if="!todo.isComplete">
    {{ todo.name }}
  </li>
</template>
```