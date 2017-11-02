# @ `web` 动画性能

## @ 动画帧

### 关于帧的概念

- 帧：在动画过程中，每一幅静止画面即为一“帧”。
- 帧率：即每秒钟播放的静止画面的数量，单位是fps(Frame per second)。
- 帧时长：即每一幅静止画面的停留时间，单位一般是ms(毫秒)。
- 跳帧(掉帧/丢帧)：在帧率固定的动画中，某一帧的时长远高于平均帧时长，导致其后续数帧被挤压而丢失的现象。

### 帧率

- 10 FPS	达成基本视觉暂留
- 25～30 FPS	传统广播电视信号
- 60 FPS 浏览器渲染刷新频率
- 60～85 HZ	显示器刷新频率
- 100 HZ	日光灯管闪烁频率

### 帧率流畅程度

- 在网页中，帧率能够达到50~60fps的动画将会相当流畅，让人倍感舒适。
- 帧率在30～50fps之间的动画，因各人敏感程度不同，舒适度因人而异。
- 帧率在30fps以下的动画，让人感觉到明显的卡顿和不适感。
- 帧率波动很大的动画，亦会使人感觉到卡顿。

## @ 小测试

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

![]()



## @ 参考

<a href="https://developers.google.com/web/fundamentals/design-and-ux/animations/">Web Fundamentals 动画</a>

<a href="http://alexorz.github.io/animation-performance-guide/">Web动画性能指南 Beta</a>
