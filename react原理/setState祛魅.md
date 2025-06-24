## setState和Component模式的setState的一些不同点
- setState通过调用lastRenderedReducer获取最新的state,和上一次的currentState，进行浅比较，如果相等，那么就退出，不重新渲染，而Component模式的setState会重新渲染
## 为什么setState要设计成为异步的、批量更新的?
这是因为每次执行setState都会触发渲染，执行一遍re-render,而re-render的流程是：
> setState=>shouldComponentUpdate=>componentWillUpdate=>render=>componentDidUpdate
这样开销太大了，所以每次执行setState都会先把它放入到一个队列中，最后一次性的批量更新。

## setState是同步还是异步的?
- setState无论是同步还是异步的，要看是否命中batchUpdate机制
- 哪些不能够命中batchUpate机制?
    - setTimeout、setInterval
    - 自定义的DOM事件
    - 总之就是React"管不到"的入口
```tsx
  handleClick() {
    // 开始处于 isBatchingUpdates ， isBatchingUpdates = true
    setTimeout(() => {
      // 此时运行 setState ， isBatchingUpdates 的值已经是 false
      this.setState({
        count: this.state.count + 1
      })
    })

    // 结束 isBatchingUpdates = false
  }
```
 