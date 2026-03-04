## 代码技巧
1. 使用Symbol.for方法注册常量，保证变量唯一性，且无法被修改
2. 使用{}：
    - 作用域隔离：提供作用域隔离，避免变量污染
    - 代码组织结构：区分生产环境以及开发环境，增强代码可读性
```javascript
function xxx(){
  {
    topLevelUpdateWarnings(container);
  }
  //...
}

```
3. 使用位运算
```javascript
var NoContext = 0;
var ConcurrentMode = 1;
var StrictMode = 2;
var ProfileMode = 4;
//在 React 中的渲染过程中，可能会同时启用并发模式和严格模式。为了表示这种组合，React 会使用按位或操作（|）来将多个模式值组合起来
var currentMode = ConcurrentMode | StrictMode; // 启用并发模式和严格模式
```
