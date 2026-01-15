## 每个hook共同逻辑
1. 每个hook初始化都会创建一个hook对象
2. 根据执行时机，区分mountXXX和updateXXX(如何区分走的是mountXXX还是updateXXX？根据current树上的memoizedState是否有当前hook对象判断，如果没值，则走mountXXX，相应的也会走到mountInProgressHook，创建一个新的hook对象,否则走updateInProgressHook)
<br>

## 为什么函数式组件需要需要hooks
1. 类式组件中this指向问题，同时类式组件的生命周期需要学习成本
2. 复用状态逻辑，靠的是HOC和Render Props这些组件设计模式，但是这些设计模式并非是万能的，它们在实现逻辑复用的同时，也破坏这组件的结构，其中最常见的一个问题就是"嵌套地狱"现象，hooks使状态逻辑复用变得简单可行。
## react-hooks使用原则
- 只在react函数中调用hook
- 不要再循环、条件或者嵌套函数中调用hook

## 为什么react-hooks的使用必须遵循一些规则
- 主要是确保hooks在每次渲染时都保持同样的执行顺序
- 在代码层面进行一个分析的话，因为Fiber节点有一个memorized属性，是一个hooks链表，每次update的时候就会去遍历这个hooks链表，举个例子：
```tsx
let isMounted=false;
const App=()=>{
    let name;
    let carreer;
    if(!isMounted){
        [name,setName]=useState('小明')
        isMounted=true;
    }
    [carreer,setCarreer]=useState('')
    return <div>
    <p>{name}</p>
    <p>{carreer}</p>
    <button onClick={()=>setName('小王')}>修改name</button>
    </div>

    //如果这样的话，首次mount的时候是没有问题的，如果点击修改name的按钮之后，后面下是的carrer的值就是小王了
}
```
> 可以通过给项目使用eslint-plugin-react-hooks插件帮助检查react语法是否遵循以上规范
