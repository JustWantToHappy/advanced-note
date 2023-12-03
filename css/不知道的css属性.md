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