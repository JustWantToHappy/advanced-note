## 绘制矩形
### 填充模式
```tsx
import React from "react";
import style from "./style/StudyCanvavs.module.scss";

const StudyCanvas = () => {
	const canvasRef = React.useRef<HTMLCanvasElement>(null);

	React.useEffect(() => {
		//找到画布
		const canvas = canvasRef.current;
		if (canvas) {
			//获取画笔上下文对象
			const ctx = canvas.getContext("2d");
			//绘制矩形
			ctx?.fillRect(0, 0, 100, 100);
            /*
            以上写法等价于:
            ctx?.rect(0,0,100,100);
            ctx?.fill();
            */
		}
	}, []);
	return (
		<div className={style.container}>
        {/*除了使用width和height属性设置宽高，也可以通过style设置宽高，注意：使用class设置会有问题*/}
			<canvas ref={canvasRef} width="500" height="500"></canvas>
		</div>
	);
};

export default StudyCanvas;

```
### 路径模式
```javascript
ctx?.strokeRect(0, 0, 100, 100);
//以上写法等价于
ctx.rect(0,0,100,100);
ctx?.stroke();

```
## ctx.clearRect
```javascript
//从坐标(0,0)开始清除，清除的矩形范围宽高分别是width,height
ctx.clearRect(0,0,width,height);
```
## beginPath与closePath
- beginPath表示下笔
- closePath相当于抬笔
```javascript
ctx.rect(100,100,200,100);
ctx.stroke();
ctx.rect(250,150,200,100);
ctx.fill();
//以上绘制出两个黑色背景填充的矩形
ctx.beginPath();
ctx.rect(100,100,200,100);
ctx.stroke();
ctx.closePath();
ctx.beginPath();
ctx.rect(250,150,200,100);
ctx.fill();
ctx.closePath();
//以上绘制出一个黑色背景填充的矩形以及一个路径模式的矩形
```
## ctx.arc(x,y,radius,开始的弧度(不是角度，是弧度)，结束的弧度，逆时针还是顺时针)
- 用于画圆弧
- 弧度角度公式：弧度=(角度*Math.PI)/180
- 默认是顺时针
- 以圆心到3点钟方向开始顺时针画弧
## ctx.moveTo
ctx.moveTo(x,y)：将画笔抬起来之后移动到(x,y)
## ctx.lineTo
ctx.lineTo(x,y)将
## ctx.strokeStyle
ctx.strokeStyle = "red";用于设置描边的颜色
## ctx.fillStyle
用于设置填充的背景色
## ctx.arcTo
除了arcTo可以画圆弧，ctx.arcTo也可以
```javascript
	//获取画笔上下文对象
			const ctx = canvas.getContext("2d");
			ctx?.beginPath();
			//设置第一个点
			ctx?.moveTo(300, 200);
			//设置第二个点和第三个点以及半径
			ctx?.arcTo(300, 250, 250, 250, 50);
			ctx?.stroke();
			ctx?.closePath();
```
## 二次贝塞尔曲线
ctx.quadraticCurveTo(cpx, cpy, x, y);
```javascript
	ctx.beginPath();
	//起始点
	ctx.moveTo(50, 20);
	//控制点和终点坐标
	ctx.quadraticCurveTo(230, 30, 50, 100);
	ctx.stroke();
	ctx.closePath();
```
### 三次贝塞尔曲线
```javascript
ctx.moveTo(50,20)//起始点
//需要两个控制点以及一个终点
ctx.bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y);
```