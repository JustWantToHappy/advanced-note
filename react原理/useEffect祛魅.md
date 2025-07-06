## mountEffect
创建update对象，挂载到fiber.updateQueue队列中<br>
比如下面的三个useEffect hook
```javascript
useEffect(()=>{
    console.log(1)
},[ props.a ])
useEffect(()=>{
    console.log(2)
},[])
useEffect(()=>{
    console.log(3)
},[])
```
![alt text](image-20.png)
### effectList
上面提到的updateQueue保存的单向链表
- 在render阶段，深度优先搜索遍历完fiber树之后，最终在fiber root上生成一条只带副作用的effect list链表
- 在commit阶段，通过遍历effect list，根据每个effect节点的effectTag类型，执行相应的dom更改
## updateEffect
## useEffect图解
