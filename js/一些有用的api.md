## matchMedia
- matchMedia("(prefers-color-schema:dark)")匹配当前系统主题是否是dark
## IntersectionObserver
提供了一种异步观察目标元素与其祖先元素或顶级文档视口交叉状态的方法，其祖先元素或视口被称为根，可以被用来实现图片懒加载还有滚动到底加载等等(用于监听元素重叠)
```typescript
const loading = document.querySelector(".loading");
	const ob = new IntersectionObserver(
		function (entries) {
			const entry = entries[0];
			//isIntersecting为true表示进入，isIntersecting表示离开
			if (entry.isIntersecting) {
				console.info("目标元素进入了，发起请求");
			}
		},
		{
			threshold: 0.1, //门槛阈值为0.1
		},
	);
	ob.observe(loading as HTMLImageElement);
```
## ResizeObserver
`ResizeObserver`接口监视Element内容盒或边框盒尺寸的变化
```html
<body>
	<div class="container"></div>
	<script>
		const container = document.querySelector(".container")
		const observer = new ResizeObserver((entries) => {
			for (const entry of entries) {
				//这里打印的是内容盒的尺寸变化
				console.log(entry.contentBoxSize);
			}
		})
		observer.observe(container)

	</script>
</body>
```