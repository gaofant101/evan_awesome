# @浮动 `(float)` [译]

## @ 什么是浮动?

CSS中的某些元素是块级元素,这意味着它们会自动启动新行.例如,如果您创建两个单词段落元素,它们将不会彼此流动,而会以不同的行显示.其他元素是内联元素.这意味着它们与以前的内容“排队”.一个例子是锚标签,它可以出现在另一个元素（如段落）中,而不会导致任何额外的空格或新行.

欺骗这种布局模式的一种方法是使用 `float` ,这允许给定的元素移动到其行的一侧,并将其他内容流下来.右浮动元素将被推到其容器的右侧,并且内容物向左下方流动,并且左浮动元素将被一直推到左侧,内容物流向右侧.

典型的例子是当你用一个段落掷出一个图像,并希望这两个图像并排出现,而不是堆叠.首先我们用一些HTML创建两个元素:
```html
<img src="http://lorempixum.com/200/200/" />
<p>Lorem ipsum...</p>
```

只要这个代码不会产生我们想要的效果.段落元素是一个块级元素,显示在其自己的行上,因此段落和图像显示在正常文档流中.

![](http://designshack.co.uk/wp-content/uploads/cssfloats101-3.jpg)

我们可以通过将图像漂浮在正确的位置来改变这种行为.

```css
img {
    float: right;
    margin: 20px;
}
```
![](http://designshack.co.uk/wp-content/uploads/cssfloats101-1.jpg)

关于这个图像的行为的一个有趣的事情现在是浮动的是我们的其他内容实际上会尝试在可能的地方围绕它.如果我们调整我们的容器或浏览器窗口的大小来缩小文本,那么文本就会自动重新放置,从而不会影响图像.

## @ 浮动规则

现在我们知道一个 `float` 是什么,以及它如何影响涉及元素的框.我们继续谈谈另外一些信息,许多开发人员可能至少不了解这些信息:管理浮动元素位置的规则.

通常情况下,开发人员将使用浮动来管理列表项的位置,也许在图像库或功能列表中.通过创建一个包含图像的简单列表,我们来看看它是如何工作的.

```html
<ul>
    <li><img src="http://placehold.it/100x100&text=1"/></li>
    <li><img src="http://placehold.it/100x150&text=2"/></li>
    <li><img src="http://placehold.it/100x100&text=3"/></li>
    <li><img src="http://placehold.it/100x100&text=4"/></li>
    <li><img src="http://placehold.it/100x100&text=5"/></li>
    <li><img src="http://placehold.it/100x150&text=6"/></li>
    <li><img src="http://placehold.it/100x100&text=7"/></li>
</ul>
```

默认情况下,所有列表项都将显示在一个大的垂直堆栈中,这显然意味着它们是块级元素.即使图像是内联元素,它们将受其父级别列表项的约束.要解决这个问题,我们可能会将列表项目浮动到左边.当一行中的多个项目浮动时,它们对内联元素流具有类似的效果.但是,正如我们将看到的,有一些关键的区别.

```css
li {
    float: left;
    margin: 4px;
}
```
![](http://designshack.co.uk/wp-content/uploads/cssfloats101-7.jpg)

但是,我们的图像高度不一样,其中有些高100像素,其他的高150像素.这导致一些严重的古怪的结果！

![](http://designshack.co.uk/wp-content/uploads/cssfloats101-8.jpg)

### 9个浮动行为规则

1. 浮动元素被推到其容器的边缘,不再进一步.
2. 任何浮动的元素都将出现在以前的浮动元素旁边或之下.如果元素悬浮在左边,则第二个元素将显示在第一个元素的右侧.如果它们正确地浮动,则第二个元素将显示在第一个元素的左侧.
3. 左浮动框不能比右侧浮动框更进一步.
4. 浮动元素不能高于其容器的顶部边缘（当涉及折叠边距时,会变得更加复杂,请参阅原始规则）.
5. 浮动元素不能高于先前的块级别或浮动元素.
6. 浮动元素不能高于前一行内联元素.
7. 另一个漂浮的元素旁边的一个浮动元素不能伸出其容器的边缘.
8. 必须将浮动盒放置得尽可能高.
9. 一个左边的浮动盒子必须尽可能地放在最左边,一个右边的浮动盒子尽可能地向右.优于比左/右更靠前的位置.

![](http://designshack.co.uk/wp-content/uploads/cssfloats101-11.jpg)

## @ 清除浮动

浮动是方便的完成一些伟大的布局功能,如创建列的内容.但是,一旦声明,它们对您可能或可能不喜欢的文档的其余部分有影响.例如,假设我们想在一个左上方的列表项之后扔入一个段落,就像我们上面那样.

![](http://designshack.co.uk/wp-content/uploads/cssfloats101-13.jpg)

结果可能不会是你希望的:

![](http://designshack.co.uk/wp-content/uploads/cssfloats101-14.jpg)

```css
p {
    clear: both;
}
```

![](http://designshack.co.uk/wp-content/uploads/cssfloats101-15.jpg)

## @ 浮动怪癖和清除修复

当给定元素只包含浮动元素时,会发生特殊的动作:父元素的高度折叠.为了说明这一点,假设我们想在我们在所有示例中使用的无序列表中放置背景颜色.如果列表中的元素没有浮动,那么我们只需要使用CSS将颜色应用到后台.

```css
ul {
    background: gray;
}
```
![](http://designshack.co.uk/wp-content/uploads/cssfloats101-18.jpg)

然而,第二个我们漂浮这些列表项,UL只包含浮动元素,所以它的高度崩溃,留下一个新手开发商想知道他的背景颜色发生了什么.

![](http://designshack.co.uk/wp-content/uploads/cssfloats101-13.jpg)

有很多方法来解决这个问题.最简单和最简单的解决方案是将显式高度应用于父元素,这是无序列表.
```css
ul {
    height: 300px;
}
```
![](http://designshack.co.uk/wp-content/uploads/cssfloats101-19.jpg)

正如你所看到的,这确实给了我们我们的背景.然而,这很少是理想的过程,只是因为如果根据内容自动计算高度,则从长远来看更为方便.如果我们现在再添加三行图像,那么这个高度是不够的.

### Clearfixes

开发人员曾经做的是在与浮动项目相同的级别上创建一个空的元素（通常是一个div）,然后将一类“clearfix”应用于该空容器.回到CSS,然后你可以在“clearfix”属性中添加清除浮点数.

```css
.clearfix {
    clear: both;
}
```
这会立即修复折叠高度问题:

![](http://designshack.co.uk/wp-content/uploads/cssfloats101-20.jpg)

这种方法的问题是没有人喜欢HTML中的额外的丑陋的元素.它根本不是语义的,这意味着它不能帮助沟通页面的清晰层次.

这个问题的新奇妙的解决方案是利用overflow属性,它控制超出其包含框的边界的内容的功能.事实证明,如果在父项目上设置溢出到隐藏或自动,它会修复高度崩溃！

```css
ul {
    overflow: auto;
}
```
![](http://designshack.co.uk/wp-content/uploads/cssfloats101-20.jpg)

这绝对是解决崩溃高度问题的最简单和最优雅的解决方案,应该是您的策略.话虽如此,有些情况下您希望将元素的溢出设置为可见,那么该怎么办?

答案是使用Nick Gallagher的Micro Clearfix Hack,它使用一些天才CSS来解决这个问题.首先,它使用:before和:after之后添加一些内容,我们可以使用它们在父进程中创建不浮动的内容.但是,您不希望在这里有任何内容,所以我们将其留空,但将显示设置为表以创建一个匿名单元格（空,占用空格）,最后使用我们的旧朋友清除.这将创建不可见的块级别项目,我们需要修复高度崩溃,而不需要额外的HTML标记.IE的旧版本需要自己的修复,所以这也被抛出.

```css
/* For modern browsers */
.cf:before,
.cf:after {
    content:"";
    display:table;
}

.cf:after {
    clear:both;
}

/* For IE 6/7 (trigger hasLayout) */
.cf {
    zoom:1;
}
```

## @ 参考

<a href="https://designshack.net/articles/css/everything-you-never-knew-about-css-floats/" target="_blank">everything-you-never-knew-about-css-floats</a>
