## 类组合选择器
```scss
//表示.container和.demo的样式都是这个
.container,.demo{}
//表示.container选择器下的子选择器.demo(有空格)
.container .demo{}
//表示同时满足.container和.demo(没有空格)
.container.demo{}
```

## is,where,not,has伪类函数
### is()&where()
```html
<style>
    .item h1,.item h2,.item p{
        color:blue;
    }
</style>
```
使用is/where代替上面的写法
```html
<style>
   .item :is(h1,h2,p){
     color:blue;
   }
    .item :where(h1,h2,p){
     color:blue;
   }
</style>
```
上面三种实现同样效果的css代码，层叠优先级分别是is>普通写法>where
使用技巧：
```html
<style>
    :is(ol, ul, menu, dir) :is(ol, ul, menu, dir) :is(ul, menu, dir) {
        list-style-type: square;
    }
</style>
```
如上这种写法就相当于组合：ol ol ul{},ol ol menu{}...

### has()
```html
<style>
h1:has(+ p) {
  margin-bottom: 0;
}

</style>
```
:has() 伪类的优先级计算方法与 :is() 和 :not() 相同

## :global
注意，:global选择器并不是css标准，它是构建工具（webpack/vite/postcss）处理的，主要作用是**CSS Modules/scoped CSS 的“全局逃逸语法”,让某些样式不要被局部作用域隔离**，举例如下：

```css
//Button.module.css
//编译前
.title {
  color:red;
}

:global(body){
  margin:0;
}

:global(.ant-btn){
  border-radius:10px;
}
//编译后
.title_a8s72 {
  color:red;
}

body {
  margin:0;
}
//不要让类名被hash
.ant-btn {
  border-radius:10px;
}

```

```html
<template>
  <div class="app">
    hello
  </div>
</template>

<style scoped>
.app{
  color:red;
}

:global(body){
  margin:0;
  background:#f5f5f5;
}
</style>
//编译后：
.app[data-v-xxxx]{
  color:red;
}

body{
  margin:0;
  background:#f5f5f5;
}
```