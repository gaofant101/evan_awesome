# @`web` 动画性能

## 动画帧

### 关于帧的概念

- 帧: 在动画过程中,每一幅静止画面即为一"帧"
- 帧率: 即每秒钟播放的静止画面的数量,单位是`fps(Frame per second)`
- 帧时长: 即每一幅静止画面的停留时间,单位一般是 `ms(毫秒)`
- 跳帧(掉帧/丢帧): 在帧率固定的动画中,某一帧的时长远高于平均帧时长,导致其后续数帧被挤压而丢失的现象

### 帧率

- `10 FPS`	达成基本视觉暂留
- `25～30 FPS`	传统广播电视信号
- `60 FPS` 浏览器渲染刷新频率
- `60～85 HZ`	显示器刷新频率
- `100 HZ`	日光灯管闪烁频率

### 帧率流畅程度

- 在网页中,帧率能够达到 `50~60fps` 的动画将会相当流畅,让人倍感舒适
- 帧率在 `30～50fps` 之间的动画,因各人敏感程度不同,舒适度因人而异
- 帧率在 `30fps` 以下的动画,让人感觉到明显的卡顿和不适感
- 帧率波动很大的动画,亦会使人感觉到卡顿

## 小测试

```html
<div class="move">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT_HdVTV5Hg_E49aaEsuVVBAxZ-XxEzjzudTTKMo0XZxVSsRWdn" width="100" height="100" alt="">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT_HdVTV5Hg_E49aaEsuVVBAxZ-XxEzjzudTTKMo0XZxVSsRWdn" width="100" height="100" alt="">
</div>
```

```css
.move{
    position: relative;
    z-index: 1;
    width: 500px;
    height: 200px;
    background: #956;
}
.move img:first-child{
    position: absolute;
    z-index: 1;
    left: 0;
    top: 0;
    transition: all 2s ease-in;
}
.move img:last-child{
    position: absolute;
    z-index: 1;
    left: 0;
    bottom: 0;
    transition: all 2s ease-in-out;
}
.move:hover img:first-child{
    left: calc(500px - 100px);
}
.move:hover img:last-child{
    transform: translateX(calc(500px - 100px));
}
```

![css3动画示例 图片有点大](https://raw.githubusercontent.com/evanhunt/evan_awesome/master/file/images/Animation.gif)

用 `css3` 来写动画
1. 首先考虑到的是要做动画的元素脱离文档流(减少重排)
2. 并设置 `z-index` 手动创建复合层(节省不设置 `z-index` 浏览器自身创建复合层)
3. 开启GPU加速 `transform-style: flat;` 、 `will-change: transform;`、  `transform: translateZ(0);`(但是这个东西并不是开启就是好的,一切都是有取舍的)
4. 优化动画的帧率,保证动画执行时间&&动画过程连贯性(先可以对着动画肉眼观察调,也可以借助 `chrome dev tool` 工具去查看每一帧的帧率进行动画视觉上的优化)
5. `css3` 的 `transform` 是好东西(`transform` 做了哪些优化为什么性能好还没有找到资料,也许是浏览器底层做的优化, 这篇文章`transform-translate-vs-top-left`做了性能对比)

# @参考

[Web Fundamentals 动画](https://developers.google.com/web/fundamentals/design-and-ux/animations/)

[Chrome 开发者工具](https://developers.google.com/web/tools/chrome-devtools/?hl=zh-cn)

[Web动画性能指南 Beta](http://alexorz.github.io/animation-performance-guide/)

[increase-your-sites-performance-with-hardware-accelerated-css](http://blog.teamtreehouse.com/increase-your-sites-performance-with-hardware-accelerated-css)

[transform-translate-vs-top-left](https://blog.tumult.com/2013/02/28/transform-translate-vs-top-left/)

[10 个原则让动画带你飞](https://github.com/xitu/gold-miner/blob/master/TODO/smooth-css-animations.md)
