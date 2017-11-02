# @ `Flex` 布局

`CSS3` 弹性盒子 (`Flexible Box` 或 `Flexbox`),是一种用于在页面上布置元素的布局模式,使得当页面布局必须适应不同的屏幕尺寸和不同的显示设备时,元素可预测地运行.
对于许多应用程序,弹性盒子模型提供了对块模型的改进,因为它不使用浮动,flex容器的边缘也不会与其内容的边缘折叠.

## @ 弹性盒布局相关

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

## @ 示例

```html
<div class="flex">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
    <div class="item">7</div>
    <div class="item">8</div>
    <div class="item">9</div>
</div>
```

```css
.flex{
    position: relative;
    z-index: 1;
    display: flex;
    width: 800px;
    height: 400px;
    background: #956;
    flex-direction: row;
}
.item{
    flex: 1;
    background: #695;
    height: 100px;
    margin-right: 10px;
    line-height: 100px;
    text-align: center;
    font-size: 20px;
    font-weight: bold;
    color: #fff;
}
```

![flex 示例 001](https://raw.githubusercontent.com/evanhunt/evan_awesome/master/file/images/flex001.png)

```
.flex{
    position: relative;
    z-index: 1;
    display: flex;
    width: 800px;
    height: 400px;
    background: #956;
    flex-direction: row-reverse;
}
```

![flex 示例 002](https://raw.githubusercontent.com/evanhunt/evan_awesome/master/file/images/flex002.png)
