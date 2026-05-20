## Promise.all
等待所有的promise完成，如果有一个失败就立即失败
## Promise.any
谁先“成功”用谁（失败的不算）
## Promise.race
谁先“结束”用谁（不管成功失败）

## promise A+规范
- .then 或 .catch 返回的值不能是 promise 本身，否则会造成死循环，例如：

```javascript
//没问题
const promise=new Promise((resolve,reject)=>resolve("error"))

promise.then((res)=>{
	return promise //看起来是返回了本身，实际上then的回调的返回值会包一层new Promise(promise)，所以返回的是一个新的promise对象，这里没有造成循环
}).then(res=>{
	console.log(res,'hhh'); //"error" "hhh"
})
//有问题
const promise = Promise.resolve().then(() => {
  return promise;//返回的是then包裹后的Promise的结果
})
promise.catch(console.err)
```