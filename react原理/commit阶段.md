## commit阶段工作流简析
- before mutation阶段:这个阶段Dom节点还没有被渲染到界面上去
- mutation:这个阶段负责DOm节点的渲染
- layout：这个阶段处理DOM渲染完毕之后的收尾逻辑，他还会吧fiberRoot的current指针指向workInProgress Fiber树
## commit阶段和双缓冲模式的联系
当workInProgress树完成commit阶段之后，FiberRoot就会切换current指针，让当前的workInProgress成为下一次更新时候的current树