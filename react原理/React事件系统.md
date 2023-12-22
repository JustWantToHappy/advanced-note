## React事件系统是如何工作的
当事件发生在具体的DOM节点上被触发后，最终都会冒泡到document上，document上所绑定的同一事件处理程序会将事件分发到具体的组件实例上
## 认识React合成事件
在底层抹平了不同浏览器之间的差异，在上层面向开发者暴露统一的、稳定的，与DOM原生事件相同的事件接口
## React事件系统工作流拆解
- 事件的绑定是在completeWork中完成的
- 事件触发的本质就是对dipatchEvent函数的调用
    - 事件触发，冒泡至document
    - 执行dispatchEvent
    - 创建事件对应的合成事件对象(SyntheticEvent)
    - 收集事件在捕获阶段所波及的回调函数和对应的节点实例
    - 将前两部步收集到的回调按照顺序执行，执行的时候SyntheticEvent会作为入参被传入每个回调
## ![Alt text](482743F2FD33B7CE58A9F431F7FC20D3.png)
- 为什么针对同一个事件，即便可能会存在多个回调，document也只需要注册一次监听？
    - 因为React最终注册到document上的并不是某一个DOM节点上对应的具体回调逻辑，而是一个统一的事件分发函数。

## 事件回调的收集与执行
1. 循环收集符合条件的父节点，存入到path数组中:traverseTwo会以当前节点(触发事件的目标节点)为起点，不断向上寻找tag====HostComponent的父节点，并将这些节点按照顺序收集进到path数组中。(path数组中子节点在前，祖先节点在后)
2. 模拟事件在捕获阶段的传播顺序，收集捕获阶段相关的节点实例和回调函数
3. 模拟事件在冒泡阶段的传播顺序，收集冒泡阶段相关的节点实例与回调函数，若该节点上对应的事件的冒泡回调不为空，那么节点实例和事件回调同样会分别被收集到SyntheticEvent._dispatchInstances和SyntheticEvent._dispatchListeners中去