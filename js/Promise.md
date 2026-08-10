## Promise状态吸收
一个 Promise 的 resolve 值如果是另一个 Promise，那么外层 Promise 不会立刻 fulfilled，而是会“吸收”内层 Promise 的状态，最终跟随内层 Promise 的结果。（koa,express这些node框架的中间件实现原理就是promise的状态吸收）
```javascript
async function test(){
	const lastPromise=new Promise(resolve=>{
		setTimeout(() => {
			resolve('result');
		}, 2000);
	})
	const state=await new Promise(resolve=>resolve(lastPromise));//外层的promsise吸收内层promise的状态
	console.log(state);//2s后输出result
}
test();
```
```javascript
const promise=new Promise(resolve=>resolve(1));

async function asyncTest(){
	//async会返回一个新的Promise对象。如果返回值也是promise，这个新的对象就会吸收返回值promise的状态
	return promise;
}

function test(){
	return promise;
}

console.log(asyncTest()===test());//false
```
## Promise.all

等待所有的promise完成，如果有一个失败就立即失败

## Promise.any

第一个fulfilled的 promise 决定结果；只有全部 reject 才会拒绝

## Promise.race

谁先“结束”用谁（不管成功失败）

## promise A+规范

- .then 或 .catch 返回的值不能是 promise 本身，否则会造成死循环，例如：

```javascript
//没问题
const promise = new Promise((resolve, reject) => resolve("error"));

promise
  .then((res) => {
    return promise; //看起来是返回了本身，实际上then的回调的返回值会包一层new Promise(promise)，所以返回的是一个新的promise对象，这里没有造成循环
  })
  .then((res) => {
    console.log(res, "hhh"); //"error" "hhh"
  });
	//死循环：TypeError: Chaining cycle detected for promise，原因解析：Promise.prototype.then会返回一个promise，而在then的回调中，promise A+规范进行了处理，如果回调函数返回值是then方法返回的promise本身，则拒绝并抛出错误
	const promise = Promise.resolve().then(() => {
		return promise; //返回的是then包裹后的Promise的结果
	});
	promise.catch(console.err);
```
