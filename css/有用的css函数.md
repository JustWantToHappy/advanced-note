## attr函数
```html
<style>
    width:attr(data-width);
    </style>
<html>
    <div data-width="100px"></div>
</html>
```

## env函数
用于获取环境变量的值
```html
    <style>
        div {
           width: env(safe-area-inset-left);
        }
    </style>
```
## clamp函数
`clamp()`函数的作用是把一个值限制在一个上限和下限之间，当这个值超过最小值和最大值的范围时，在最小值和最大值之间选择一个值使用。它接收三个参数：最小值、首选值、最大值。
```scss
font-size: clamp(1rem, 2.5vw, 2rem);
```
- 当2.5vw大于2rem的时候，使用2rem
- 当2.5vw小于1rem的时候，使用1rem
- 其他使用2.5vw