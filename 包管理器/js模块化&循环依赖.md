## js模块化的几种方式
- CommonJs
- AMD
- CMD
- UMD
- ESM

下面介绍一些重要的模块化方式

## esm
ESM（ECMAScript Modules）是 ECMAScript 6（即 ES2015）引入的模块化机制，旨在为 JavaScript 提供 原生 的模块系统

esm的优势：
1. 静态分析与优化，由于import,export是静态的，使得tree shaking成为可能，减少最终产物体积
2. 在浏览器环境中，ESM 默认是 异步加载 的，不会阻塞页面渲染。每个模块会在需要时动态加载
3. 作用域隔离：每个es模块都有自己的作用域，不会影响全局作用域，减少命名冲突
4. 单一默认导出

支持的环境：
- 浏览器已经原生支持 ESM（不过在老旧浏览器中需要 polyfill 或使用构建工具）
- Node.js 从 12.x 版本开始支持 ESM，14.x 以上版本已是稳定支持

## UMD
兼容 CommonJS、AMD、全局变量
```javascript
//math.umd.js

// math.umd.js (UMD 格式)
(function (root, factory) {
  if (typeof define === 'function' && define.amd) {
    // AMD
    define([], factory);
  } else if (typeof exports === 'object') {
    // CommonJS
    module.exports = factory();
  } else {
    // 浏览器全局
    root.MathLib = factory();
  }
}(this, function () {
  return {
    add: function(a, b) {
      return a + b;
    },
    PI: 3.14
  };
}));

```
```html
<!-- 浏览器直接使用 -->
<script src="math.umd.js"></script>
<script>
  console.log(MathLib.add(2, 3)); // 5
</script>

```

```javascript
//nodejs中使用
const MathLib = require('./math.umd.js');
console.log(MathLib.add(2, 3)); // 5
```

## esm和umd格式产物
- .mjs 文件约定俗成就是 ES Module（ESM） 格式
- .umd.js为umd格式产物，通常作为通用分发文件
> 一些库（比如 React、Lodash）会提供同时支持 UMD 和 ESM 的构建产物

## CommonJs的循环依赖
**require导入**：把导出的值复制一份，放到一块新的内存中。

commonjs通过模块缓存来解决，每一个模块都先加入缓存后执行，每次遇到require就先检查缓存，这样就不会出现死循环

**多次引用**：同样因为缓存，一个模块不会被多次执行
```javascript
//index.js
var a = require('./a')
var b= require('./b')

// a.js
module.exports.a = '原始值-a模块内变量'
console.log('a模块执行')
var c = require('./c')

// b.js
module.exports.b = '原始值-b模块内变量'
console.log('b模块执行')
var c = require('./c')

// c.js
module.exports.c = '原始值-c模块内变量'
console.log('c模块执行')

//打印结果：a模块执行，c模块执行，b模块执行
```

## ESM的循环依赖
**export导出**:ES Module导出的是一份值的引用，CommonJS则是一份值的拷贝。也就是说，CommonJS是把暴露的对象拷贝一份，放在新的一块内存中，每次直接在新的内存中取值，所以对变量修改没有办法同步；而ES Module则是指向同一块内存，模块实际导出的是这块内存的地址，每当用到时根据地址找到对应的内存空间，这样就实现了所谓的“动态绑定”。

```javascript
// b.mjs
export let count = 1;
export function add() {
  count++;
}
export function get() {
  return count;
}

// a.mjs
import { count, add, get } from './b.mjs';
console.log(count);    // 1
add();
console.log(count);    // 2
console.log(get());    // 2
```

```javascript
// a.js
let count = 1;
module.exports = {
  count,
  add() {
    count++;//修改的原内存中的count
  },
  get() {
    return count;//获取原内存中的count
  }
};

// index.js
//获取到是内存的一份拷贝
const { count, add, get } = require('./a.js');
console.log(count);    // 1
add();
console.log(count);    // 1
console.log(get());    // 2
```
**esm原理：**ES Module借助模块地图，已经进入过的模块标注为获取中，遇到import语句会去检查这个地图，已经标注为获取中的则不会进入，地图中的每一个节点是一个模块记录，上面有导出变量的内存地址，导入时会做一个连接——即指向同一块内存。


## 如何查找模块？
查找模块时，核心模块和文件模块的查找都比较简单，对于react/vue这种第三方模块，会从当前目录下的node_module文件下开始，递归往上查找，找到该包后，根据package.json的main字段找到入口文件。