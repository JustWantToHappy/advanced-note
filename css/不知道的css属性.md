## columns
用于设置元素的列宽和列数
```html
<style>
    .container{
        columns:3;
    }
    .container{
        columns:6rem;
    }
</style>
```
## filter
滤镜
- 灰阶滤镜grayscale(1)
- 设置阴影:drop-shadow,使用方式类似box-shadow，与box-shadow不同的是：
    - box-shadow是针对整个盒子来设置阴影
    - drop-shadow是仅仅针对这个区域中的像素点来设置阴影
## backdrop-filter
这个css属性可以让你为一个元素后面的区域添加图形效果，如模糊或者颜色偏移，因为它适用于元素背后所有的元素
> 基本使用:backdrop-filter: blur(2px);

## resize
```html
/*可以手动控制div*/
<style>
    div{
        resize: both;
		overflow: auto;
    }
</style>
```

## width:fit-content
容器宽度由内容决定，这里建议不要使用inline-block，因为行盒坑多。
```html
<style>
    div{
        width:fit-content;
    }
</style>
```

## css容器查询
```html
<style>
    .post {
  container-type: inline-size;
  container-name: sidebar;
}
@container sidebar (min-width: 700px) {
  .card {
    font-size: 2em;
  }
}
</style>
```
## 媒体查询
```html
<style>
/*表示当屏幕小于640px的时候*/
@media not all and (min-width: 640px) { ... }
/*表示当屏幕大于等于640px的时候,两种写法*/
@media (min-width: 640px) { ... }
@media screen and (min-width:640px){...}
/*当暗黑模式下可以在这里面设置css变量的值用于切换主题*/
@media (prefers-color-scheme: dark){}
</style>
```
## attr()函数
```html
<style>
    width:attr(data-width);
    </style>
<html>
    <div data-width="100px"></div>
</html>
```

## env函数
用于获取环境变量的值
```html
    <style>
        div {
           width: env(safe-area-inset-left);
        }
    </style>
```
## intial
作用：用于设置默认值，如果某个css属性的默认值不清楚，则通过inital可以设置：
> line-height:intital;

## unset
作用：给css属性设置这个值之后，如果这个属性能继承就会继承，不能继承就会使用默认值
## revert
作用：把css属性设置成为浏览器的一个默认值.并不是w3c的默认值,比如：
```html
<style>
    .default{
        .all:revert;
    }
</style>
```
## margin-inline-start
margin-left的作用
## margin-inline-end
margin-right的作用
## writing-mode
定义了文本水平或垂直排布以及在块级元素中文本的行进方向
- horizontal-tb:
## animation-direction
animation-direction CSS 属性设置动画是应正向播放、反向播放还是在正向和反向之间交替播放。
```html
<style>
    .container{
        animation:demo linear 1s infinite alternate;
    }
    //往返运动
    @keyframes demo{
        from{
            transform:tranlateY(-10px);
        }
        to{
            transform:translateY(10px);
        }
    }
</style>
```
## animation-timing-function
- 值可以是ease,linear,ease-in-out,ease-in
- 值可以是steps函数
- 值可以是贝塞尔函数
## clamp函数
`clamp()`函数的作用是把一个值限制在一个上限和下限之间，当这个值超过最小值和最大值的范围时，在最小值和最大值之间选择一个值使用。它接收三个参数：最小值、首选值、最大值。
```scss
font-size: clamp(1rem, 2.5vw, 2rem);
```
- 当2.5vw大于2rem的时候，使用2rem
- 当2.5vw小于1rem的时候，使用1rem
- 其他使用2.5vw

## white-space
white-space 属性用于设置如何处理元素内的空白字符。
```html
<style>
    /**
    不换行
    */
    white-space:nowrap;
</style>
```
## word-break
```html
<style>
    word-break:break-word;//强制换行
word-break:break-all;//允许单词内部换行
word-break:keep-all//允许单词之间换行
</style>
```
## text-shadow
用于设置文字阴影,每个阴影值由元素在 X 和 Y 方向的偏移量、模糊半径和颜色值组成。
```html
text-shadow: 1px 1px 2px pink;
```
## background-position
- 一个值的用法用来指定把这个项目（原文为 item）放在哪一个边界。另一个维度被设置成 50%，所以这个项目（原文为 item）被放在指定边界的中间位置。
```html
<style>
    .container{
        background-position:top;
    }
</style>
```

## box-shadow
如果没有指定`inset`，默认阴影在边框外，即阴影向外扩散
```html
/* 插页 (阴影向内) | x 偏移量 | y 偏移量 | 阴影颜色 */
box-shadow: inset 5em 1em gold;
```

## aspect-ratio
aspect-ratio CSS 媒体属性 可以用来测试 viewport 的宽高比。也可以用来设置图片的宽高比
```css
/* 最小宽高比 */
@media (min-aspect-ratio: 8/5) {
  div {
    background: #9af; /* blue */
  }
}
```
