## 纯css实现瀑布流
```html
<style>
    .container{
        display:grid;
        grid-template-columns:repeat(4,1fr);
        grid-gap:10px;
        grid-template-rows:masonry;//主要代码，这是实验属性
    }
</style>
<div class="container">
    <img src='1.jpg'>
    <img src="2.jpg">
</div>
```
> 建议使用js实现
## css变量使用技巧
```javascript
//给css变量--c1设置属性值#fff
html.style.setAttribute("--c1","#fff");
可以使用一些库提取出图片主要的背景颜色，然后通过这种方式给页面设置背景色(图片调色盘)
```
```html
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
	<style>
		:root {
			--color: red;
			--color-secondary: green;
		}
	</style>
</head>

<body>
	<div style="color:var(--color)" id="app">这是文字</div>
</body>
<script>
	const app = document.querySelector("#app")
	app.style.color = "var(--color-secondary)"
</script>

```

## 使用js实现高度的自动过渡效果
```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
	<style>
		.container {
			width: 100px;
			background-color: red;
			color: white;
			word-break: break-word;
			transition: all linear 0.3s;
		}
	</style>
</head>

<body>
	<div class="container"></div>
	<button style="margin-top: 100px;">toggle</button>

</body>
<script>
	const container = document.querySelector('.container');
	const button = document.querySelector('button');
	button.addEventListener('click', () => {
		container.textContent = "这是一段文字，这段文字的长度超过了容器的宽度，所以会自动换行。"
		container.style.height = "auto"
		const height = container.offsetHeight;
		container.style.height = '0px'
		const textContent = container.textContent;
		requestAnimationFrame(() => {
			container.style.height = `${height}px`
		})
	});
</script>

</html>
```