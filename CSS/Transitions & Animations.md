# @ `Transitions` & `Animations`

`CSS3` 引入 `Transitions` & `Animations` 能是的前端开发人员具备了交互能力.

`CSS3 Transitions`,你可能会在发生状态变化时更改元素的外观和行为,例如,当它被悬停,聚焦,活动或定位时.

`CSS3 Animations` 允许在多个关键帧中更改元素的外观和行为.转换提供从一个状态到另一个状态的变化,而动画可以在不同的关键帧上设置多个转换点.

## @ `Transitions`

如前所述,为了进行转换,元素必须有状态变化,并且必须为每个状态识别不同的样式.用于确定不同风格的最简单的方法是使用 `:hover` , `:focus` , `:active` ,和 `:target` 伪类.

有总共四个转型相关的属性,包括 `transition-property` , `transition-duration` , `transition-timing-function` ,和 `transition-delay` .不是所有这些都需要建立一个过渡,前三个是最受欢迎的.

在下面的示例中,盒子将以二次方式改变其 `background `颜色.

```css
.box {
    background: #2db34a;
    transition-property: background;
    transition-duration: 1s;
    transition-timing-function: linear;
}
.box:hover {
    background: #ff7b29;
}

```

### 过度的属性

该 `transition-property` 属性决定什么属性将结合其他过渡性质被改变.默认情况下,元素不同状态中的所有属性将在更改后更改.但是,只有在 `transition-property` 值内识别的属性将受到任何转换的影响.

在上面的示例中, `background` 属性在 `transition-property` 值中标识.这里的 `background` 财产是唯一的属性将改变在1二次的持续时间 `linear` .任何其它性质改变,当一个元件的状态,但不包括在内包含 `transition-property` 的值,将不接收作为设定由过渡行为 `transition-duration` 或 `transition-timing-function` 特性.

如果需要转换多个属性,那么它们可以在该 `transition-property` 值内以逗号分隔.另外,关键字值 `all` 可以用于转换元素的所有属性.

```css
.box {
    background: #2db34a;
    border-radius: 6px
    transition-property: background, border-radius;
    transition-duration: 1s;
    transition-timing-function: linear;
}
.box:hover {
    background: #ff7b29;
    border-radius: 50%;
}

```

### 过渡时间

使用 `transition-duration` 属性设置转换发生的持续时间.此属性的值可以使用常规时序值(包括 `seconds(s)` 和 `milliseconds(ms)` 设置.例如,这些定时值也可以进行分数测量 `.2s`.

转换多个属性时,您可以设置多个持续时间,每个属性一个.与 `transition-property` 属性值一样,可以使用逗号分隔值声明多个持续时间.当确定个人属性和持续时间时,这些值的顺序是重要的.例如,属性中标识的第一个属性 `transition-property` 将与属性中标识的第一个属性匹配 `transition-duration` ,等等.

如果正在转换多个属性,只有一个持续时间值被声明,则该值将是所有转换属性的持续时间.

```css
.box {
    background: #2db34a;
    border-radius: 6px;
    transition-property: background, border-radius;
    transition-duration: .2s, 1s;
    transition-timing-function: linear;
}
.box:hover {
    background: #ff7b29;
    border-radius: 50%;
}

```

### 过渡期间的移动方式

该 `transition-timing-function` 属性用于设置转换将移动的速度.了解从 `transition-duration` 属性的持续时间,转换可以在单个持续时间内具有多个速度.几对比较流行的关键字值的 `transition-timing-function` 特性包括 `linear` , `ease-in` , `ease-out` ,和 `ease-in-out`.

 `linear` 关键字值标识在过渡恒定速度移动,从一个状态到另一个.该 `ease-in` 值标识一个缓慢启动并在整个转换过程中加速的转换,而该 `ease-out` 值标识了一个在整个转换过程中快速启动并且减慢的转换.该 `ease-in-out` 值标识一个缓慢开始的转换,在中间加速,然后在结束前再次减慢.

每个定时功能都有一个立方贝尔曲线,可以使用该 `cubic-bezier(x1, y1, x2, y2)` 值进行专门设置.附加值包括 `step-start` , `step-stop` 和唯一标识的 `steps(number_of_steps, direction)` 值.

转换多个属性时,您可以识别多个定时功能.这些定时功能值与其他转换属性值一样可以被声明为逗号分隔值.

```css
.box {
    background: #2db34a;
    border-radius: 6px;
    transition-property: background, border-radius;
    transition-duration: .2s, 1s;
    transition-timing-function: linear, ease-in;
}
.box:hover {
    background: #ff7b29;
    border-radius: 50%;
}

```

### 过渡延迟

在声明过渡属性,持续时间和计时功能之上,您还可以使用 `transition-delay` 属性设置延迟.延迟设置一个时间值(秒或毫秒),用于确定在执行之前停止转换的时间.与所有其他转换属性一样,为了延迟大量转换,每个延迟都可以声明为逗号分隔值.

```css
.box {
    background: #2db34a;
    border-radius: 6px
    transition-property: background, border-radius;
    transition-duration: .2s, 1s;
    transition-timing-function: linear, ease-in;
    transition-delay: 0s, 1s;
}
.box:hover {
    background: #ff7b29;
    border-radius: 50%;
}

```

## @ `Animations`

### 动画关键帧

要设置元素应该进行转换的多个点,请使用 `@keyframes` 规则.该 `@keyframes` 规则包括动画名称,任何动画断点以及要动画化的属性.

```css
@keyframes slide {
    0% {
        left: 0;
        top: 0;
    }
    50% {
        left: 244px;
        top: 100px;
    }
    100% {
        left: 488px;
        top: 0;
    }
}

```

### 动画名称

一旦动画的关键帧已被声明,则需要将其分配给一个元素.为此,该 `animation-name` 属性与动画名称一起使用,从 `@keyframes` 规则中标识为属性值.该 `animation-name` 声明被应用于其中动画是要被施加到的元素.

```css
.stage:hover .ball {
    animation-name: slide;
}
```

### 动画持续时间

一旦 `animation-name` 在元素上声明了属性,动画就像转换一样.如果需要,它们包括持续时间,定时功能和延迟.要开始,动画需要使用 `animation-duration` 属性声明的持续时间.与转换一样,持续时间可以在几秒或几毫秒内设置.

```css
.stage:hover .ball {
    animation-name: slide;
    animation-duration: 2s;
}
```

### 动画迭代

默认情况下,动画从头到尾运行一次循环,然后停止.要使动画重复自己多次, `animation-iteration-count` 可以使用属性 `.animation-iteration-count` 属性的值包括整数或 `infinite` 关键字.使用整数将重复动画多次指定,而 `infinite` 关键字将无限期地以无止境的方式重复动画.

```css
.stage:hover .ball {
    animation-name: slide;
    animation-duration: 2s;
    animation-timing-function: ease-in-out;
    animation-delay: .5s;
    animation-iteration-count: infinite;
}

```

### 动画方向

除了能够设置动画重复的次数之外,您还可以使用 `animation-direction` 属性声明动画完成的方向.为价值观 `animation-direction` 财产包括 `normal` , `reverse` , `alternate` ,和 `alternate-reverse` .

该 `normal` 值以开始到结束的方式播放动画.该 `reverse` 值将播放与 `@keyframes` 规则中确定的完全相反的动画,从而开始100%并向后工作0%.

该 `alternate` 值将向前播放动画,然后向后播放.内包括向前运行的关键帧0%来100%向后从后100%到0%.使用 `animation-iteration-count` 属性可能会限制动画向前和向后运行的次数.计数开始于1运行动画转发0%到100%,然后将1向后运行的动画100%来0%.组合2一次迭代.该 `alternate` 值也反转任何时序功能.如果一个动画使用了 `ease-in` 从去值0%到100%,它然后使用 `ease-out` 从去值100%来0%.

最后,该 `alternate-reverse` 值结合了值 `alternate` 和 `reverse` 值,然后向后运行动画.该 `alternate-reverse` 值从100%运行开始,0%然后100%再次返回.

```css
.stage:hover .ball {
    animation-name: slide;
    animation-duration: 2s;
    animation-timing-function: ease-in-out;
    animation-delay: .5s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
}
```

### 动画播放状态

该 `animation-play-state` 属性允许动画将被播放或使用暂停 `running` 和 `paused` 分别关键字值.当您播放暂停的动画时,它将从当前状态恢复运行,而不是从一开始就重新开始.

在下面的例子中 `animation-play-state` 属性被设置为 `paused` 使得当 `stage` 通过点击激活它.请注意,在放开鼠标之前,动画将暂时暂停.

```css
.stage:hover .ball {
    animation-name: slide;
    animation-duration: 2s;
    animation-timing-function: ease-in-out;
    animation-delay: .5s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
}
.stage:active .ball {
    animation-play-state: paused;
}
```

### 动画填充模式

该 `animation-fill-mode` 属性标识在运行动画之前,之后或之前和之后元素的样式.该 `animation-fill-mode` 属性接受四种关键字值,包括 `none`,`forwards`,`backwards`,和`both`.

`none`在运行动画之前或之后,该值不会对元素应用任何样式.

该 `forwards` 值将保留在最后指定的关键帧内声明的样式.这些样式可能,但是,可以通过受影响的 `animation-direction` 和 `animation-iteration-count` 属性值,究竟哪里改变动画结束.

`backwards` 在运行动画之前,该值将在识别后立即应用于第一个指定关键帧内的样式.这包括在可能在动画延迟期间设置的任何时间应用这些样式.该 `backwards` 值也可能受到 `animation-direction` 属性值的影响.

最后,该`both`值将应用来自值 `forwards` 和 `backwards` 值的行为.

```css
.stage:hover .ball {
    animation-name: slide;
    animation-duration: 2s;
    animation-timing-function: ease-in-out;
    animation-delay: .5s;
    animation-fill-mode: forwards;
}
.stage:active .ball {
    animation-play-state: paused;
}
```

## @ 参考

<a href="https://developers.google.com/web/fundamentals/design-and-ux/animations/" target="_blank">Web Fundamentals 动画</a>

<a href="https://learn.shayhowe.com/advanced-html-css/transitions-animations/" target="_blank">transitions-animations</a>
