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

