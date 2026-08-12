## BFC
BFC：块级格式化上下文，一个独立的渲染区域，该区域有一套渲染规则来约束块级盒子的布局。**BFC是一个独立的布局环境，BFC内部的元素布局与外部互不影响**
 
BFC的布局规则有如下几条：
1. 内部的Box会在垂直方向上一个接一个放置
2. Box垂直方向上的距离由margin决定，属于同一个BFC的两个相邻的Box的margin会发生重叠
3. 每个盒子的左外边框紧挨着包含块的左边框，即使浮动元素也是如此
4. BFC的区域不会与浮动Box重叠
5. 计算BFC高度的时候，浮动子元素也参与计算
> body就是一个天然的BFC

如何将Box单独设置成为一个BFC?（常用方式）
1. float不是none
2. position:absolute/fixed
3. overflow:auto/scroll/hidden
4. 行内块元素：display:inline-block
5. 弹性盒子：display:flex/inline-flex
6. 网格元素：dispaly:grid/inline-grid

## IFC、GFC、FFC
- IFC:行内格式化上下文
- GFC：网格布局格式上下文
- FFC：弹性格式格式化上下文
