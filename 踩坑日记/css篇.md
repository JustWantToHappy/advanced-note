## 选择器的误区
如下两种选择器表示的含义是不同的
```html
<style>
    .container.demo {
        width: 100px;
        height: 100px;
        background-color: red;
    }
    //这里是有空格的
    .container .demo{
        ...
    }
</style>
```
## 行内盒和行内块的空格问题
如下这两种方式布局是有区别的，因为html的换行默认就是一个空格，所以第一种方式图片之间是有空隙的，但是第二种是没有空隙的，解决方案就是使用浮动，flex，网格布局等
```html
<style>
    .container.images img {
        width: 100px;
    }
</style>
<div class="container images">
    <img src="./images/qqavatar.jpg" />
    <img src="./images/qqavatar.jpg" />
    <img src="./images/qqavatar.jpg" />
</div>
```
```html
	<div class="container images">
		<img src="./images/qqavatar.jpg" /><img src="./images/qqavatar.jpg" /><img src="./images/qqavatar.jpg" />
	</div>
```