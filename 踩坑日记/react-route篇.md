## 路由懒加载的坑
lazy方法只支持默认导出
```ts
const { Home } = React.lazy(() => import("@/pages"));//错误写法
const Home=React.lazy(()=>import("@pages/Home"))//正确写法
```