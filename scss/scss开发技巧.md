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
## 切换主题色通用方案
```scss
//通过scss语法实现主题切换

$currentTheme:'';

$themes :(
light:(
bgColor:#fff,
textColor: #000
),
dark:(
bgColor: #000,
textColor: #fff
)
);

@mixin useTheme(){
@each $themeName,$theme in $themes{
//修改全局的$currentTheme变量
$currentTheme: $themeName !global;

//下面的&表示当前的选择器
html[data-theme='#{$themeName}'] &{
@content;
}
}
}

@function getVar($varName){
//当前主题对应的变量值
@return map-get(map-get($themes,$currentTheme),$varName);
}

//某个元素使用主题样式:
.item{
@include useTheme{
background: getVar(bgColor);
color: getVar(textColor);
}
}

//编译结果如下：

html[data-theme=light] .item {
  background: #fff;
  color: #000;
}
html[data-theme=dark] .item {
  background: #000;
  color: #fff;
}
```