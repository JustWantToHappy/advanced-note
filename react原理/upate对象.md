## 思考
挂载可以理解为一种特殊的更新，ReactDOM.render和setStat也是一种触发更新的姿势
## update的创建
1. dispatchAction(创建update)
2. scheduleUpdateOnFiber(调度update)
    - enqueuUpdate调用：将update入队
    - 在render阶段，upduateQueue的内容会成为render阶段计算Fiber节点的新state的依据。 
2. performSyncWorkOnRoot(render阶段)
3. commit阶段
## 与Fiber的联系
每一个Fiber节点都有一个对应的upateQueue，这个updateQueue存储着update对象
## scheduleUpdateOnFiber如何区分同步还是异步？
通过lane标记判断，如果是同步，则通过performSyncWorkOnRoot方法开启render阶段，如果是异步，则通过performConcurrentWorkOnRoot开启render阶段