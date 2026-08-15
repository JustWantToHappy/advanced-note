## eval的基本用法
eval()函数接收一个字符串作为参数,该字符串可以是一个js表达式、语句或者一系列语句的字符串
```javascript
eval(`var a=1,b=2;
if(a<b){
	console.log("a<b");
}else{
	console.log("a>b");
}`)
```
如果eval()的参数不是字符串，eval()会将参数原封不动返回，例如：
```javascript
console.log(eval(true));//true
var a=5;
console.log(eval(a));//5
```
### eval作用域
eval里面的代码在当前词法环境中执行，因此它可以看到外部变量
```javascript
let a=1;

function f(){
	let a=2;
	eval("console.log(a)")//2
}
f();
```
它也可以改变外部变量
```javascript
let x=10;
eval("x=20;")
console.log(x);//20
```
严格模式下，eval有自己的词法环境，因此，在eval内部声明的函数和变量在外部不可见
```javascript
"use strict"
eval("let x=5;")
console.log(typeof x);//undefined
```
### 永远不要使用eval
- eval是一个危险的函数，它使用与调用者相同的权限执行代码，如果你用eval运行的字符串代码被恶意修改，会在用户计算机上运行恶意程序
- eval运行更慢，因为它必须调用js解释器，使用eval往往比普通js代码慢几个数量级

