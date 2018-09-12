# @外边距坍塌 `(margin)` [译]

W3C规范定义如下塌陷边距:"在本说明书中,表达式折叠边距意味着两个或更多个框(可能彼此相邻或嵌套)的相邻边距(无空的内容,填充或边框区域或间隙分开)合并形成单边距".

## 规则

简单来说,这个定义表明
- 当两个元素的垂直边距相互接触时,只有具有最大边距值的元素的边距才能得到兑现,而具有较小边距值的元素的边距将被折叠为零.
- 在一个元素具有负余量的情况下,将余量值相加在一起以确定最终值.
- 如果两者均为负值,则使用较大的负值.此定义适用于相邻元素和嵌套元素.

还有其他元素没有折叠的情况:
- 浮动元素
- 绝对定位的元素
- 内嵌块元素
- 具有溢出的元素设置为除可见之外的任何元素(它们不会与子元素折叠边距).
- 已清除的元素(它们不会将其顶部边距与其父块的底边缘折叠起来).
- 根元素

## 相邻元素之间的边缘缩小

边缘在相邻元素之间崩溃.简单来说,这意味着对于正常文档流程中的相邻垂直块级元素,只有具有最大边距值的元素的边距才能被保证,而具有较小边距值的元素的边距将被折叠为零.例如,如果一个元素具有25px底部边距,并且其下方的元素具有20px顶部边距,则仅执行25px底部边距,并且元素将保持25px彼此相距的距离.他们不会像45px(25 + 20),可以预期的那样.

```css
h1 {
    margin: 0 0 25px 0;
    background: #cfc;
}
p {
    margin: 20px 0 0 0;
    background: #cf9;
}
```

![](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/04/1398314844css-box-model_collapsing-margins.png)

元素之间的差距只有25px更小,边距已经缩小为零.如果在上面的例子中,元素的边距相等(比如说每个都有20个像素),那么它们之间的距离就只有这个20px.

## 父母和子元素之间的边缘缩小

到目前为止,我们只处理了相邻元素的崩溃效应,但对于边缘接触的父母和子女来说,相同的过程也是如此."触摸”是指相邻边距之间不存在填充,边框或内容的地方.在以下示例中,父元素具有设置顶部边距的子元素:

```css
h1 {
    margin: 0;
    background: #cff;
}
div {
    margin: 40px 0 25px 0;
    background: #cfc;
}
p {
    margin: 20px 0 0 0;
    background: #cf9;
}
```
![](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/04/1398314904css-box-model_collapsing-margins2.png)

实际上,如果我们的div元素没有顶部边距,并且p元素有一个,我们将得到相同的结果40px margin-top.该40px margin-topp元素上有效地成为的div元素的上边距,并推动股利下降的页面40px,留下p顶部紧贴嵌套元素.段落上面的div元素上没有可见的背景.

为了显示两个元素的顶部边距,并且为了在元素上方显示div元素的背景p,将需要一个边框或填充来阻止边距的折叠.如果我们只是向div元素添加一个顶部边框,我们可以实现我们原来寻找的效果:

```css
h1 {
    margin: 0;
    background: #cff;
}
div {
    margin: 40px 0 25px 0;
    background: #cfc;
    border-top: 1px solid #000;
}
p {
    margin: 20px 0 0 0;
    background: #cf9;
}
```

![](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/04/1398314949css-box-model_collapsing-margins3.png)

# @参考

[collapsing-margins](https://www.sitepoint.com/collapsing-margins/)

[what-you-should-know-about-collapsing-margins](https://css-tricks.com/what-you-should-know-about-collapsing-margins/)
