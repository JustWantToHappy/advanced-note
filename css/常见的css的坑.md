## position:fixed

position:fixed不一定就是相对窗口进行定位的，如果祖先元素开启了transform,那么元素就会相对于祖先元素，比如：

```html
<style>
  .container {
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

在文档流中，父容器的高度默认是子元素撑开的，即子元素有多高，父容器就是有多高，但是如果给子元素设置了浮动之后，子元素就会完全脱离文档流，此时子元素无法撑开父容器，父元素高度塌陷，解决方法可以设置父元素的overflow不为visiable等等(原理就是触发 BFC 的容器都会自动「包裹」内部浮动元素)

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
  .mask {
    inset: 0;
    position: fixed;
    background-color: rgba(0, 0, 0, 0.2);
  }
</style>
```

## flex布局下省略号不生效

参考如下文章：https://juejin.cn/post/6885949601170325511

## 滚动穿透

当一个弹窗或遮罩层（通常是固定定位）覆盖在页面上时，用户在弹窗上滑动手指，页面底层的元素也会跟着滚动，就好像滚动事件“穿透”到了下面一样

# 外边距合并
1. 兄弟元素之间
```css
  .top { margin-bottom: 30px; }
  .bottom { margin-top: 20px; }
  /* 实际间距是 max(30, 20) = 30px，而不是 50px */
```
2. 父子之间
```css
  .parent { margin-top: 0; }
  .child { margin-top: 30px; }
  /* 如果父元素没有 border/padding/overflow 隔离，30px 会"穿透"到父元素 */
```
3. 空元素自身
```css
  .empty { margin-top: 20px; margin-bottom: 30px; }
  /* 上下 margin 会合并为 30px */
```
触发条件：
- 必须是垂直方向上，水平方向上不会合并
- 必须是块级元素，inline元素不会
- 必须在同一个BFC中

解决外边距合并有如下方法：
| 方法 | 适用场景 | 具体做法 | 示例 |
|------|----------|----------|------|
| 设置 BFC | 父子重叠 | 给**父元素**创建 BFC | `.parent { overflow: hidden; }` |
| 设置 BFC | 兄弟重叠 | 给**其中一个兄弟**包裹一层 BFC 容器 | `<div style="overflow:hidden"><p>兄弟1</p></div>` |
| 添加边框或内边距 | 父子重叠 | 给**父元素**加 border 或 padding | `.parent { border: 1px solid transparent; }` 或 `.parent { padding: 1px; }` |
| 使用 Flexbox/Grid | 兄弟重叠 | 给**父容器**设置弹性/网格布局 | `.parent { display: flex; flex-direction: column; }` |
| 直接改用 padding | 父子重叠 | 删掉**子元素**的 margin，改在**父元素**上设 padding | `.parent { padding-top: 30px; }`（子元素不再设 margin-top）
|
| 使用空元素隔离 | 兄弟重叠 | 在**两个兄弟之间**插入一个带 `display: flow-root` 的空容器 | `<div style="display:flow-root"></div>` 或使用伪元素`::before { content: ''; display: table; }` |

> 父子 margin 塌陷发生的前提是：父元素和子元素之间「没有任何阻挡」