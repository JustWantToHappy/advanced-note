## 基本概念
- 路由(以Route为代表):负责定义路径与组件之间的映射关系
- 导航(以Link为代表):负责触发路径的改变
- 路由器则会根据Route定义出来的映射关系为新的路径匹配它对应的逻辑
## 前端路由解决了什么问题？
- SPA其实并不知道当前的页面"进展到了哪一步",你必须重复之前的操作才可以重新对内容进行定位————SPA并不会"记住"你的操作
- 有且仅有一个URL给页面做映射,这对SEO并不够友好
- 拦截用户的刷新操作，避免服务端盲目响应，返回不符合预期的资源内容
- 感知URL的变化
## hash模式
```javascript
window.addEventListener("hashchange",(e)=>{})
```
## history模式
`history.pushState()//向浏览历史中追加一条记录`
`history.replaceState()//修改(替换)当前页在浏览历史中的信息`
```javascript
window.addEventListener("popstate",(e)=>{})
```
**go、forward和back等方法的调用确实会触发popstate,但是pushState和replaceState不会**