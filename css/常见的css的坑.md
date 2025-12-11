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
## 父容器高度塌陷
在文档流中，父容器的高度默认是子元素撑开的，即子元素有多高，父容器就是有多高，但是如果给子元素设置了浮动之后，子元素就会完全脱离文档流，此时子元素无法撑开父容器，父元素高度塌陷，解决方法可以设置父元素的overflow不为visiable
## css3中sticky不生效的原因
- 父元素不能够设置为overflow:hidden或者overflow:auto的属性(这里的父元素可以是嵌套的)
- 必须指定top、bottom、left以及right其中之一
- 父元素的高度不能够低于sticky元素的高度
## 滚动条无法被遮罩层遮住的原因
- 不要在根节点上添加滚动条，而是自己写一个块,比如react.App
- 块有了，给这个块设置与屏幕宽高相等的宽度和高度。
- 添加遮罩层，遮罩层宽高与屏幕宽高也相等
```html
//蒙层基本样式
<style>
.mask{
    inset:0;
    position:fixed;
    background-color:rgba(0,0,0,.2);
}
</style>
```
## flex布局下省略号不生效
参考如下文章：https://juejin.cn/post/6885949601170325511

## 滚动穿透
当一个弹窗或遮罩层（通常是固定定位）覆盖在页面上时，用户在弹窗上滑动手指，页面底层的元素也会跟着滚动，就好像滚动事件“穿透”到了下面一样

# 外边距合并
默认情况下，父元素和第一个or最后一个元素之间的垂直外边距会发生外边距合并（也可以发生在一个元素自身的外边距，比如marginTop和marginBottom）

解决外边距合并有如下方法：
1. 给父元素添加边框
2. 给父元素添加内边距
3. 使用overflow属性
4. 使用浮动或者定位