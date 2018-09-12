# @`CSSOM` 是什么

## 什么是`CSSOM`

- `CSSOM`代表 `CSS` 对象模型
- 它基本上是在网页上找到的 `CSS` 样式的“地图”
- 它非常像 `DOM`,而是 `CSS` 而不是 `HTML`
- `CSSOM`与 `DOM` 结合使用浏览器来显示网页

![](https://varvy.com/performance/images/cssom-defined.png)

`CSSOM`对于页面渲染至关重要.
它是关键渲染路径的基本核心部分,并且了解它的作用是 `Web` 性能优化的重要组成部分(使网页加载速度更快).

## `CSSOM` 是做什么的？

`CSSOM` 将样式表中的规则映射到页面对应的元素上.

虽然 `CSSOM` 采取了复杂的措施来做这件事,但是 `CSSOM` 最终的功能还是将样式映射到它们应该对应的元素上去.

更确切地说,`CSSOM`识别 `tokens` 并把这些 `tokens` 转换成一个树结构上的对应的结点.所有结点以及它们所关联的页面中的样式就是所谓的 `CSS Object Model`

## `Web` 浏览器使用 `CSSOM` 去渲染页面

`Web` 浏览器为了展示页面,需要经历以下四个步骤：

- 检查 `HTML` 并构建 `DOM`
- 检查 `CSS` 并构建`CSSOM`
- `Web`浏览器将 `DOM` 和 `CSSOM` 结合,并构建出 `render tree`
- 展示 `Web` 页面

从上述四个步骤可以看出, `CSSOM` 对于 `Web` 页面的展示起着重要作用

你不必为了优化你的 `Web` 页面而去了解 `CSSOM` 是怎样工作的,这里有几个关于 `CSSOM` 的关键点你需要知道,利用这些关键点可以优化页面的加载速度.

- `CSSOM` 阻止任何东西渲染
- `CSSOM` 在加载一个新页面时必须重新构建
- 页面中 `CSS` 的加载和页面中 `javascript` 的加载是有关系的

### `CSSOM` 阻止任何东西渲染

所有的 `CSS` 都是阻塞渲染的(意味着在 `CSS` 没处理好之前所有东西都不会展示).

真的原因是,如果浏览器在 `CSS` 检查之前展示了页面,那么每个页面都是没有样式的,等一会之后又突然有了样式,整个页面的体验就会很糟糕.

![](https://user-gold-cdn.xitu.io/2017/2/17/50e49e197b06c7567cd641e0db5c013c?imageView2/0/w/1280/h/960/ignore-error/1)

由于`CSSOM`被用作创建 `render tree` ,那么如果不能高效的利用 `CSS` 会有一些严重的后果.

主要的后果就是你的页面在加载时白屏.

### `CSSOM` 在加载一个新页面时必须重新构建

这可能对你来说,或明显或不明显,但这是一非常关键的点.

这意味着即使你的 `CSS` 文件被缓存了,也并不意味着这个已经构建好了的 `CSSOM` 可以应用到每一个页面.

当用户跳到你的另一个页面时(即使浏览器缓存了所有需要的 `CSS` ),`CSSOM` 也必须重新构建一遍.

也就是说,如果你的 `CSS` 文件写得很蹩脚,或者体积很大,这也会对你页面加载产生负面的影响.

### 页面中 `CSS` 的加载和页面中 `javascript` 的加载是有关系的

`javascript` 的加载可能会阻塞`CSSOM`的构建

简单来说,`CSSOM` 是展示任何东西的必需品.在 `CSSOM` 构建之前,所有东西都不会展示,如果你阻塞了 `CSSOM` 的构建, `CSSOM` 的构建就会消耗更长的时间,这就意味着页面的渲染也需要更长的时间.
如果你的 `javascript` 阻塞了`CSSOM`的构建,你的用户就会面对更长时间的白屏.

## 影响 `CSSOM` 的一般优化方式

这里有几个首屏优化的最佳实践,可以帮助你让 `CSSOM` 构建地快一些(也就是让页面加载更快)

- Optimize your [critical rendering path](https://varvy.com/pagespeed/critical-render-path.html)
- Make sure your pages are calling [stylesheets before javascripts](https://varvy.com/pagespeed/style-script-order.html)
- Ensure you are [optimizing CSS delivery](https://varvy.com/pagespeed/optimize-css-delivery.html)

# @参考

[What is CSSOM?](https://varvy.com/performance/cssom.html)
