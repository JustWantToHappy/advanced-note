## css文档流
css中有三种基本的定位机制：普通流，浮动流，定位流

文档流：可以理解为元素的一种状态，处于这种状态下的元素具有一些特性。说白了，标准文档流就是一个“默认”状态，即元素排版布局过程中，元素会自动从左往右，从上往下的流式排列。并最终窗体自上而下分成一行行，并在每行中从左至右的顺序排放元素。

### 浮动
![alt text](image-5.png)
```html
<style>
		* {
			margin: 0px;
			padding: 0px;
		}

		.float1 {
			float: left;
			background-color: red;
		}

		.float2 {
			float: left;
			background-color: green;
		}
	</style>
		<div class="float1">
		这是一段文字1
	</div>
	<div class="float2">
		这是一段文字2
	</div>
```
浮动元素脱离文档流之后默认会贴靠，如何让不同的浮动元素不贴靠：清除浮动实现，如下是主要方式：
![alt text](image-6.png)
1. 给需要清除浮动的元素添加clear属性
```css
	.float2 {
		float: left;
		background-color: green;
		/* 不允许左边出现浮动元素 */
		clear: left;
	}
```
2. 隔墙法：在两个浮动元素之间添加一个clear:both(不允许元素左右存在浮动元素)的元素
```html
	<div class="float1">
		这是一段文字1
	</div>
	<div style="clear:both;"></div>
	<div class="float2">
		这是一段文字2
	</div>
```
3. 给浮动元素的父元素添加高度（注意：父元素的高度要大于浮动元素的高度）
4. 给浮动元素的父元素设置overflow:hidden
```html
<style>
		.app1 {
			overflow: hidden;
		}

		.app2 {
			overflow: hidden;
		}

		.float1 {
			float: left;
			background-color: red;
		}

		.float2 {
			float: left;
			background-color: green;
		}
	</style>

	<div class="app1">
		<div class="float1">
			这是一段文字1
		</div>
	</div>
	<div class="app2">
		<div class="float2">
			这是一段文字2
		</div>
	</div>
```
4. 最流行的方式：通过给浮动元素添加伪元素，以及设置伪元素的一系列属性
```html
	<style>
		* {
			margin: 0px;
			padding: 0px;
		}

		.float1 {
			float: left;
			background-color: red;
		}

		.app1::after {
			content: "";
			display: block;
			clear: both;
		}

		.float2 {
			float: left;
			background-color: green;
		}
	</style>
		<div class="app1">
		<div class="float1">这是一段文字1</div>
	</div>
	<div class="float2">这是一段文字2</div>
```
### 脱离文档流
Q: 脱离文档流就不占据空间了吗？

A: 可以这么说。更准确地一点说，是一个元素脱离文档流（out of normal flow）之后，其他的元素在定位的时候会当做没看见它，两者位置重叠都是可以的。

元素脱离文档流后的变化：
1. 块元素
- 若一个块元素脱离文档流，它下面的，处于文档流中的兄弟元素会上移；
- 多个块元素可以在同一行（比如都设置浮动）；
- 块元素被内容撑开，也就是说，width的默认值不是父元素的width。

2. 内联元素
可以设置width和height（变成了块元素）。

总结：脱离文档流，也就是将元素从普通的布局排版中拿走，不占据位置（悬空了），其他盒子在定位的时候，会当做脱离文档流的元素不存在而进行定位。需要注意的是，使用float脱离文档流时，其他盒子会无视这个元素，但其他盒子内的文本依然会为这个元素让出位置，环绕在周围。而对于使用position脱离文档流的元素，其他盒子与其他盒子内的文本都会无视它