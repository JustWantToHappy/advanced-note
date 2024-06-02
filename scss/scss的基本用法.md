## 数学运算
```scss
//除法运算
@use "sass:math";
$width:math.div(100,10)px
//编译结果
--width:1px;
```

## &
&表示当前选择器
```scss
@mixin useTheme(){
    html[data-theme="dark"] &{
        background:red;
        color:#fff;
    }
}
.item{
    @include useTheme;
}
//编译结果
html[data-theme="dark"] .item{
    //...
}
```

## 继承
@extend

```scss
.error {
    border: 1px solid red;
    background-color: #fdd;
}

.seriousError {
    @extend .error;
    border-width: 3px;
}
//编译结果：
.error,.seriousError {  
  border: 1px solid red;  
  background-color: #fdd;  
}  
  
.seriousError {  
  border-width: 3px;
}
```

## 函数
```scss
@function getBgColor(){
    @return red;
}
```
## 条件判断
```scss
p {
  @if 1 + 1 == 2 { border: 1px solid; }
  @if 5 < 3 { border: 2px dotted; }
  @if null  { border: 3px double; }
}
//编译结果：
p {
  border: 1px solid; 
}
```
```scss
$type: monster;
p {
  @if $type == ocean {
    color: blue;
  } @else if $type == matador {
    color: red;
  } @else if $type == monster {
    color: green;
  } @else {
    color: black;
  }
}
```

## 循环
@for
```scss
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}
//编译结果
.item-1 {
  width: 2em;
}
.item-2 {
  width: 4em; 
}
.item-3 {
  width: 6em; 
}
```
@while

```scss
$i: 6;
@while $i > 0 {
  .item-#{$i} { width: 2em * $i; }
  $i: $i - 2;
}
//编译结果
.item-1 {
  width: 12em;
}
.item-2 {
  width: 8em; 
}
.item-3 {
  width: 4em; 
}
```
