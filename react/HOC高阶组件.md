## HOC种类
- 属性代理
- 反向继承
## 几种包装强化组件的方式

- mixin模式：react初期提供的一种组合方法，通过React.createClass，加入mixins属性，类似vue中的mixins
- 衍生方式：其实就是通过原型继承的方式
- extends继承方式
- **HOC模式**
- 自定义hooks模式：主要针对无状态组件
## HOC解决的问题

- 复用逻辑：HOC就像一个加工react组件的工厂，批量对原有组件进行加工，包装处理
- 强化props:高阶组件返回的组件，可以劫持上一层传过来的props，然后混入新的props，用来增强组件的供能
- 赋能组件:HOC有一项独特的特性，就是可以给HOC包裹的业务组件，提供一些拓展功能，比如说**额外的生命周期，额外的事件**
- 控制渲染：可以对原来的组件，进行条件渲染，节流渲染，懒加载等功能。
## 如何编写HOC?
### 装饰器模式
```tsx
@withStyles(styles)
@withRouter
@keepaliveLifeCycle
class Index extends React.Componen{
    /* ... */
}
```
### 无状态组件
```tsx
function Index(){
    /* .... */
}
export default withStyles(styles)(withRouter( keepaliveLifeCycle(Index) )) 
```
## 正向属性代理

- 就是给组件包裹一层代理组件
### 优点

- 正常属性代理可以和业务组件低耦合，零耦合，对于条件渲染和props增强，只负责控制子组件渲染和传递额外的props就行，目前开源的HOC基本上都是提供通过这个模式实现。
- 同样适用于class声明的组件和function声明的组件。
- 可以嵌套使用
- 可以完全隔离业务组件的渲染，相比于反向继承，属性代理这种模式，可以完全控制业务组件渲染与否，可以避免反向继承带来的一些副作用，比如生命周期的执行。
### 缺点

- 一般无法直接获取到业务组件的状态，如果想要获取，需要使用ref获取组件的实例。
- 无法直接继承静态属性，如果需要继承需要手动处理，或者引入第三方库。
```tsx
function HOC(WrapComponent){
    return class Advance extends React.Component{
       state={
           name:'alien'
       }
       render(){
           return <WrapComponent  { ...this.props } { ...this.state }  />
       }
    }
}
```
```tsx
class Index extends React.Component{
  render(){
    return <div> hello,world  </div>
  }
}
Index.say = function(){
  console.log('my name is alien')
}
function HOC(Component) {
  return class wrapComponent extends React.Component{
     render(){
       return <Component { ...this.props } { ...this.state } />
     }
  }
}
const newIndex =  HOC(Index) 
console.log(newIndex.say)//undefined

```
## 反向继承
### 优点

- 方便获取组件的内部状态，比如:state，props，生命周期，绑定的事件函数等。
- es6继承可以良好继承静态属性，我们无需对静态属性和方法进行额外的处理。
### 缺点

- 无状态组件无法使用
- 如果多个反向继承HOC嵌套在一起，当前状态会覆盖上一个状态，这样带来的隐患是非常巨大的。比如有多个componentDidMount，当前componentDidMount覆盖上一个componentDidMount
```tsx
class Index extends React.Component{
  render(){
    return <div>hello,world</div>
  }
}
function HOC(Component){
//直接继承需要包装的组件
return class wrapComponent extends Component{
	}
}
export default HOC(Index)

```
