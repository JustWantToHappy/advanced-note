## 如何在其他scss文件中使用global.css的公共变量和公共样式
- vite:
```javascript
//vite.config.js|ts
{
    css: {
		preprocessorOptions: {
			scss: {
				additionalData: `@import "@/assets/styles/global.scss";`, // 你需要注入的资源文件路径
			},
		},
	},
}
```
- webpack:好像要下载(sass-resources-loader)，然后配置一下webpack


## mixin中的插槽
@content;
```scss
.flex($justifiyContent,$alignItems){
	display:flex;
	justify-content:$justifyContent;
	align-items:$alignItems;
	@content;
}

.header{
	@include flex(center,center){
		width:100%;
		height:100%;
	}
}
```