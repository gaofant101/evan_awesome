# @`Flex`

`CSS3` 弹性盒子 (`Flexible Box` 或 `Flexbox`),是一种用于在页面上布置元素的布局模式,使得当页面布局必须适应不同的屏幕尺寸和不同的显示设备时,元素可预测地运行.
对于许多应用程序,弹性盒子模型提供了对块模型的改进,因为它不使用浮动,flex容器的边缘也不会与其内容的边缘折叠.

## 弹性盒布局相关

![](https://mdn.mozillademos.org/files/12998/flexbox.png)

### 弹性容器 `(Flex container)`

包含着弹性项目的父元素.通过设置 `display` 属性的值为 `flex` 或 `inline-flex` 来定义弹性容器.

### 弹性项目 `(Flex item)`

弹性容器的每个子元素都称为弹性项目.弹性容器直接包含的文本将被包覆成匿名弹性单元.

### 轴 `(Axis)`

每个弹性框布局包含两个轴.弹性项目沿其依次排列的那根轴称为主轴 `(main axis)`.垂直于主轴的那根轴称为侧轴 `(cross axis)`.

### 方向 `(Direction)`

弹性容器的主轴起点 `(main start)`/主轴终点 `(main end)` 和侧轴起点 `(cross start)`/侧轴终点 `(cross end)` 描述了弹性项目排布的起点与终点.它们具体取决于弹性容器的主轴与侧轴中,由 `writing-mode` 确立的方向（从左到右、从右到左,等等）.

### 行 `(Line)`

根据 `flex-wrap` 属性,弹性项目可以排布在单个行或者多个行中.此属性控制侧轴的方向和新行排列的方向.

### 尺寸 `(Dimension)`

根据弹性容器的主轴与侧轴,弹性项目的宽和高中,对应主轴的称为主轴尺寸 `(main size)` ,对应侧轴的称为 侧轴尺寸 `(cross size)`.

## 属性

### `flex-direction`

```css
.box {
    flex-direction: column | column-reverse | row | row-reverse;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)

- row(默认值): 主轴为水平方向,起点在左端
- row-reverse: 主轴为水平方向,起点在右端
- column: 主轴为垂直方向,起点在上沿
- column-reverse: 主轴为垂直方向,起点在下沿

### `flex-wrap`

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071006.png)

```css
.box{
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```

#### `nowrap`(默认): 不换行

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071007.png)

#### `wrap`: 换行,第一行在上方

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg)

#### `wrap-reverse`: 换行,第一行在下方

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071009.jpg)

### `flex-flow`

```css
.box {
    flex-flow: <flex-direction> || <flex-wrap>;
}
```

### `justify-content`

```css
.box {
    justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

- `flex-start` (默认值): 左对齐
- `flex-end`: 右对齐
- `center`:  居中
- `space-between`: 两端对齐,项目之间的间隔都相等
- `space-around`: 每个项目两侧的间隔相等 所以,项目之间的间隔比项目与边框的间隔大一倍

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)


### `align-content`

```css
.box {
    align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)

- `flex-start`: 与交叉轴的起点对齐
- `flex-end`: 与交叉轴的终点对齐
- `center`: 与交叉轴的中点对齐
- `space-between`: 与交叉轴两端对齐,轴线之间的间隔平均分布
- `space-around`: 每根轴线两侧的间隔都相等所以,轴线之间的间隔比轴线与边框的间隔大一倍
- `stretch`(默认值): 轴线占满整个交叉轴


## 项目属性

### `order`

```css
.item {
    order: <integer>;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071013.png)

### `flex-grow`

```css
.item {
    flex-grow: <number>; /* default 0 */
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)

### `flex-shrink`

```css
.item {
    flex-shrink: <number>; /* default 1 */
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg)

如果所有项目的 `flex-shrink` 属性都为1,当空间不足时,都将等比例缩小.如果一个项目的 `flex-shrink` 属性为0,其他项目都为1,则空间不足时,前者不缩小.

### `flex-basis`

```css
.item {
    flex-basis: <length> | auto; /* default auto */
}
```

### `flex`

`flex` 属性是 `flex-grow`, `flex-shrink` 和 `flex-basis` 的简写,默认值为 `0 1 auto`.后两个属性可选.

```css
.item {
    flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

### `align-self`

`align-self` 属性允许单个项目有与其他项目不一样的对齐方式,可覆盖 `align-items` 属性。默认值为 `auto`,表示继承父元素的 `align-items` 属性,如果没有父元素,则等同于 `stretch`

```css
.item {
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png)

## 左边固定, 右边自适应 示例

```html
<div class="demo">
	<div class="left">左边固定宽度为100px，这里设置了高度为auto</div>
	<div class="right">右边宽度自适应，并且左右两个区域是等高的，这里设置了高度为200px</div>
</div>
```

```css
.demo{
	display: flex;
}

.demo .left{
	width: 100px;
	min-width: 100px;
	max-width: 100px;
	height: auto;
	background: #B4D3F7;
	flex-grow: 0;
}

.demo .right{
	margin-left: 10px;
	width: auto;
	height: 200px;
	background: #F7E8B4;
	flex-grow: 1;
}
```
[Demo](https://jsfiddle.net/evan_g/scef649h/)

## `flexboxfroggy`

一个学习 `flex` 布局的课程, [FLEXBOX FROGGY](https://flexboxfroggy.com/)

# @参考

[使用 CSS 弹性盒子](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes)
