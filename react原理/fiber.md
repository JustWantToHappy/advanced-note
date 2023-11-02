## 作用
将一个大的更新任务拆分成一个个小的更新任务，每当执行完一个fiber执行单元之后，渲染线程就会将主线程交回去，看看有没有更高优先级的任务，如果有优先级更高的任务，确保其他任务不会被饿死。如果没有则判断当前帧有没有空余时间，如果有的话就会执行下一个fiber，没有就会将主线程交给浏览器
## 特征
Fiber架构的重要特征就是可以被打断的异步渲染模式，根据“能否被打断”这一标准，React16的生命周期被划分为了render和commit阶段
## 生命周期对应的阶段
- render函数以及之前的生命周期函数都是对应的render阶段
- getSnapshotBeforeUpdate方法以及无状态组件中的useLayoutEffect都是对应的pre-commit阶段
- commit阶段包括：react更新dom和ref，以及之后的生命周期：componentDidMount,componentDidUpdate等
---
**render阶段在执行过程中允许被打断，而commit阶段则总是同步执行的，**

## 思考
 为什么render阶段在执行过程中可以被打断？<br>
`这是因为render阶段是在内存中执行的，对于用户是不可见的`

为什么commit阶段是同步执行的，不可以被打断?<br>
`这是因为Fiber树的切换是基于双缓存的，一个是页面上显示的Fiber树对应的dom树，另一个是内存中已经构建好的离屏树，因为这个阶段用户是可见的，所以这里必须同步执行，切换fiber树`

**为什么componentWillMount,componentWillUpate,componentWillReceiveProps这几个生命周期会被废除？**<br>
`这是因为它们都处于render阶段，都可能被重复执行(有可能Fiber会被多次执行)，如果在这里面进行发送请求等操作，则会造成不可估计的后果`

> react16改造生命周期的主要动机是为了配合Fiber架构带来的异步渲染机制