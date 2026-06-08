## 基本概念
- 路由(以Route为代表):负责定义路径与组件之间的映射关系
- 导航(以Link为代表):负责触发路径的改变，如果是传统多页面应用，点击a标签就会请求跳转后的页面，单应用的Link组件需要阻止这个行为
```text
点击 Link
     ↓
preventDefault
     ↓
不发送请求
     ↓
pushState修改URL
     ↓
Router更新状态
     ↓
React重新渲染
```
- 路由器则会根据Route定义出来的映射关系为新的路径匹配它对应的逻辑
## 前端路由解决了什么问题？
在单页应用中，用 URL 来描述页面状态，并在不刷新浏览器的情况下完成页面切换，同时保留浏览器前进后退、刷新、分享链接等能力。
## hash模式
```javascript
window.addEventListener("hashchange",(e)=>{})
```
## history模式
`history.pushState()//向浏览历史中追加一条记录，会改变地址url，不会重新加载页面`
`history.replaceState()//修改(替换)当前页在浏览历史中的信息，会改变地址url，不会重新加载页面`
```javascript
window.addEventListener("popstate",(e)=>{})
```
**go、forward和back等方法的调用确实会触发popstate,但是pushState和replaceState不会，history.back/forward/go 会优先尝试 bfcache（浏览器的一种缓存机制，直接“恢复现场”，而不是重新加载页面）当页面满足“可安全冻结与恢复”的条件时才会使用，否则就退化为普通页面重新加载。比如no-store或者不安全访问的时候就会重新加载**

实现前端路由的伪代码：
```javascript
const routes = {
  "/": Home,
  "/user": User,
  "/article": Article
}

function render() {
  const pathname = window.location.pathname

  const Component = routes[pathname]

  ReactDOM.render(
    <Component />,
    root
  )
}

export const history = {
  push(path) {
    window.history.pushState({}, "", path)

    render()
  }
}

window.addEventListener(
  "popstate",
  render
)

render()
```