## 概念
JSDOC是文档注释，jsDoc是一种统一的注释规范，它以/**或者/***开头，以*/结尾
## type
```javascript
/**
 * @type {number}
 */
let a;//number
```
## returns
```javascript
/**
 * 
 * @returns {Function} 返回一个函数
 */
function bbb() {
	return function () {

	}
}
```
## param
```javascript
/***
 * @param {Object} a
 * @param {string} a.name 名称
 * @param {number} a.age 年龄
 */
function demo(a) {

}

```
## 自定义类型typedef
```javascript
//正确写法
/**
 * @typedef TableRow
 * @property {number} age
 * @property {string} name
 */
/**
 * @type TableRowa
 */
let a;

//错误写法
/**
 * @typedef TableRow
 * @property {number} age
 * @property {string} name
 * @type TableRow
 */
let a;
```
## ts中的注释
ts注释不需要指定类型
```typescript
import React from "react";
/**
 *使用防抖动的函数
 *
 * @param fn 需要进行防抖的函数
 * @param delay 延迟时间，默认是100ms
 * @param immediate 是否立即执行，默认是false
 * @returns 返回防抖之后的函数
 */
export function useDebouce<T extends (...args: unknown[]) => unknown>(
	fn: T,
	delay = 100,
	immediate = false,
) {
	const timerRef = React.useRef<ReturnType<typeof setTimeout> | null>();

	const debouceFn = React.useCallback(
		(...args: unknown[]) => {
			...
		},
		[fn, delay, immediate],
	);

	return debouceFn;
}

```