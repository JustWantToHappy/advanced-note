## 脱水
指的是在服务端渲染页面的时候，将页面的状态和数据序列化为JSON格式，并嵌入到html中，这样，在页面初次加载的时候，客户端可以直接获取到初始状态，而不需要再次向服务器请求数据，这有助于提高页面加载性能。
## 水合
在客户端进行导航的时候，将之前序列化的状态和数据还原到客户端应用程序中
---
Next.js v12 之前的 SSR 都是通过 getServerSideProps这样的方法，在页面层级获取数据，然后通过 props 传给每个组件，然后将整个组件树在服务端渲染为 HTML。

但是 HTML 是没有交互性的（non-interactive UI），客户端渲染出 HTML 后，还要等待 JavaScript 完全下载并执行。JavaScript 会赋予 HTML 交互性，这个阶段被称为水合（Hydration）。此时内容变为可交互的（interactive UI）
## SSR
服务端渲染
## CSR
客服端渲染
## SSG(用于生成单个静态文件)
静态站点生成：在构建的时候生成，可用cdn缓存
## ISR(可以用于生成多个静态文件)
增量静态再生:在构建时生成静态文件，并按需更新他们，在ISR模式下，开发者可以给每个页面都设置一个重新验证的时间。当用户访问该页面的时候，如果页面自上次构建以来还没达到重新验证的时间，Next.js 将服务该页面的静态版本。如果已经达到或超过了设定的时间，Next.js 会在后台重新生成页面，并更新静态文件。这个过程对用户来说是透明的，用户总是会立即看到页面的一个版本，要么是缓存版本，要么是新生成的版本。可使用cdn缓存
## RSC
TODO:流媒体的传输方式可以后面去了解一下。
服务端组件+客户端组件+流媒体传输的方式(这里应该用的是分块传输)
