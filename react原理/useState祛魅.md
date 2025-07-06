## setState和Component模式的setState的一些不同点
- setState通过调用lastRenderedReducer获取最新的state,和上一次的currentState，进行浅比较，如果相等，那么就退出，不重新渲染，而Component模式的setState会重新渲染
## useState和useReducer的共性和区别
- 同:
  - useState和useReducer都是使用dispatchAction触发函数更新

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
## useState对应的hook对象结构
```javascript
const hook={
  memoizedState:'当前最新的值',
  baseState:'后续计算更新使用的基础值',
  queue:{
    pending:{
      //环状链表：最后一个节点的next指向第一个节点，queue.next指向最新的update对象
      next:null,
      //函数或者表达式：比如state=>state+1,state+1等
      action:null
    }
  },
  //结构与queuePending类似，但是它是一个无环链表，因为最后一个节点的next指向null
  baseQueue:{
    next:null,
    action:null,
  },
  //连接下一个hook对象
  next:null,
}
```
<br>
<strong>为啥有了queue.pending还需要baseQueue?</strong>
<br>
这里举个简单的例子：
<br>

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  const handleLowPriority = () => {
    // 低优先级更新
    setTimeout(() => {
      setCount(c => c + 1);
      setCount(c => c + 1);
    }, 1000);
  };

  const handleHighPriority = () => {
    // 高优先级更新
    setCount(c => c + 10);
  };

  return (
    <>
      <button onClick={handleLowPriority}>低优先级+2</button>
      <button onClick={handleHighPriority}>高优先级+10</button>
      <div>{count}</div>
    </>
  );
}
```
如果先点击'低优先级+2',再点击'高优先级+10'，此时低优先级更新还未执行被打断，如果只有一个链表存储，就会丢失低优先级的更新，因为react会优先处理高优先级更新

```javascript
// 1. 低优先级更新进入 queue.pending
queue.pending = {
  action: c => c + 1,
  action: c => c + 1
}


// 2. React开始处理这些更新，将它们移入baseQueue
baseQueue = {
  action: c => c + 1,
  action: c => c + 1
}
baseState:2

// 3. 高优先级更新进来了，中断了当前的低优先级更新
// 高优先级更新进入 queue.pending
queue.pending = {
  action: c => c + 10
}

// 4. baseQueue保存了之前的低优先级更新
// 这样在处理完高优先级更新后
// React可以回来继续处理这些低优先级更新
```
## useState图解
> hook的共同点
1. 每个hook初始化都会创建一个hook对象
2. 根据执行时机，区分mountXXX和updateXXX
