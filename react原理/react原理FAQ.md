- 注册调度任务和执行任务回调是不同时执行的，<mark>一旦所有的状态更新任务都被添加到调度队列中之后，React会开始执行任务回调</mark>，并且任务的执行可能会在多个事件循环中分散开来。对于每一个任务回调，React会检查他对应的组件是否仍然处于挂载阶段，如果组件已经卸载，任务回调会被忽略，不再执行。
- 在真实的hook中，组件mount时候的hook和update时的hook来自不同的对象，如下：
```javascript
// mount时的Dispatcher
const HooksDispatcherOnMount: Dispatcher = {
  useCallback: mountCallback,
  useContext: readContext,
  useEffect: mountEffect,
  useImperativeHandle: mountImperativeHandle,
  useLayoutEffect: mountLayoutEffect,
  useMemo: mountMemo,
  useReducer: mountReducer,
  useRef: mountRef,
  useState: mountState,
  // ...省略
};

// update时的Dispatcher
const HooksDispatcherOnUpdate: Dispatcher = {
  useCallback: updateCallback,
  useContext: readContext,
  useEffect: updateEffect,
  useImperativeHandle: updateImperativeHandle,
  useLayoutEffect: updateLayoutEffect,
  useMemo: updateMemo,
  useReducer: updateReducer,
  useRef: updateRef,
  useState: updateState,
  // ...省略
};
```
- jsx会被编译为React.createElement,React.createElement会返回一个叫做"ReactElement"的js对象，例如:
```tsx
import React from 'react'
<div className='text'>text</div>
//以上jsx会被编译为:
React.createElement('div',{className:'text'},'text')
```

- 为啥react通过fakeNode触发事件的形式执行一些操作
1. 方便统一调度入口，插入一些公共逻辑
2. 在开发环境下捕获用户代码（组件 render、生命周期、事件回调等）里抛出的异常（有些浏览器在try-catch之后，window.onerror不能监听到错误，而使用fakeNode自定义事件派发的方式，可以监听到事件）