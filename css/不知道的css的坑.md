## position:fixed
position:fixed不一定就是相对窗口进行定位的，如果祖先元素开启了transform,那么元素就会相对于祖先元素，比如：
```html
<style>
.container{
    transform: translateX(200px);
    width: 400px;
    height: 400px;
    background-color: red;
}

.son {
    position: fixed;
    top: 0;
    left: 0;
    width: 20px;
    height: 20px;
    background-color: pink;
}   
</style>
<div class="container">
		<div class="son"></div>
</div>
```