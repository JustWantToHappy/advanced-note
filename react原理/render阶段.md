## 渲染流水线
![Alt text](image-14.png)
## performaceUnitOfWork方法
通过循环调用performUnitOfWork方法来触发beginWork方法，新的Fiber节点就会不断被创建
```javascript
function workLoopSync(){
    while(workInProgress!==null){
        perfomaceUnitOfWork(workInProgress);
    }
}
```
## 第一次beginWork
在react首次渲染时，进入到render阶段之前已经存在了fiberRoot对象和current树的FiberRoot对象，因此第一次beginWork的时候，也就是创建workInProgress树的FiberRoot对象时，执行的是update逻辑。
## beginWork
- beginWork的入参是一对alternate连接起来的workInProgress和current节点
- 开启Fiber节点创建过程(传入Fiber，创建子Fiber)
    - 通过调用reconcileChildren方法，生成当前节点的子节点(这个方法会根据current是否为null判断进入到mount阶段还是update阶段)
        - 如果current为null:
        ```javascript
        workInProgress.child=mountChildFibers(workInProgress,null,...)
        ```
        - 如果current不为空:
        ```javascript
        workInProgress.child=reconcileChildFibers(workInProgress,current.child,...)
        ```
    - 在mount和update阶段都会调用ChildReconciler，这个方法的入参是布尔值(表示是否要处理副作用)，返回reconcilerChildFibers和mountChildFibers两个不同的函数，<font style="color:#fff;background-color:green">这两个函数的不同在于对副作用的处理不同</font>
    ![Alt text](image-15.png)
    - ChildReconciler中定义了大量的形如placeXXX，deleteXXX,updateXXX,reconcileXXX等这样的函数，这些函数覆盖了对Fiber节点的创建，增加，删除，修改等操作，将直接或者间接被reconcileChildFibers调用
- rootFiber可以看作是App组件的父节点
![Alt text](image-13.png)