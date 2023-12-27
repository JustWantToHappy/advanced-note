## 除法运算
- div中两个参数是否带单位：
    - 都带上单位没有问题
    - 除数带上单位，被除数不带单位没有问题
    - 除数不带单位，被除数带上单位，报错
```scss
@use "sass:math";
//将宽度分成了多少份
$part:100;
//设计稿宽度
$width:750px;
@function toRem($px){
	@return #{math.div($px,$width)*$part}rem;
}

.container{
	width:toRem(75px);
	background-color: red;
}

```