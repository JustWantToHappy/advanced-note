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
 * @returns {Function}
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
 * @param {string} a.name
 * @param {number} a.age
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