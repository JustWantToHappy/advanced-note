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
### 全局容器查询
```html
@media (max-width:300px){
    .card h2 {
    font-size: 2em;
  }
}
```
### 局部容器查询
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