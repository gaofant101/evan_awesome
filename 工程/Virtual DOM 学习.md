# @`Virtual DOM`

> 对官方对`virtual dom`的记忆理解

## 动机

在 `react` 中 `render()`创建 `react` 元素树; 在下一个 `state || props`更新时, `render()`将创建一个不同的 `react`元素树. 此时`react` 需要弄清楚如何有效的更新`UI`来匹配最新的元素树.

`react`做了一个大胆的假设:
- 不同的类型的元素会产生不同的元素树
- 通过`key`来优化对比效率

## 差异算法 `diffing algorithm`

在区分两颗元素树的时候, 首先会比较根元素. 不同元素类型, 行为也不一样.

### 不同类型的元素

当根元素是不同类型时, `react` 将卸载旧的元素树从头开始构建新的元素树.旧组件卸载时将调用 `componentWillUnmount()`清除旧组件中所有的状态.

```diff
# 根元素不同, 从新构建元素树
- <div>
-       <ComponentA />
- <div>

+ <span>
+       <ComponentA />
+ <span>
```

### 相同类型的 `react dom` 元素

比较相同类型的 `react dom`, 保持相同底层的 `dom`的节点, 仅更新需要更新的属性.

```diff
<div
    style={{
-        color: 'red',
        fontWeight: 'bold'
    }}
/>

<div
    style={{
+        color: 'green',
        fontWeight: 'bold'
    }}
/>

```

### 相同类型的组件元素

当组件更新时, 实例保持不变, 以便渲染保持状态. 此时调用 `componentWillReceiveProps() componentWillUpdate()`;

`render()` 调用, `diff`算法新旧树进行递归对比;

### 子节点的递归

`react` 同时对两个子节点进行迭代时, 发现差异时突变;

```diff
<ul>
    <li>first</li>
    <li>second</li>
</ul>

<ul>
    <li>first</li>
    <li>second</li>
+    <li>third</li>
</ul>

// 对比<li>first</li> <li>second</li> 2个节点
// 发现<li>third</li>差异, 执行插入操作
```

如果只是按序操作那么执行操作很简单, 但是实际情况并不会这么简单

```diff
<ul>
    <li>Duke</li>
    <li>Villanova</li>
</ul>

<ul>
    <li>Connecticut</li>
    <li>Duke</li>
    <li>Villanova</li>
</ul>
// <li>Duke</li> 第一个节点对比不一样
// 删除每一个节点, 然后重新构建新的节点
// 实际上只是新增了一个节点
// 这样对性能有极大的浪费
```

### `key`

为了解决低效率的问题, `react` 中设计了 `key`属性.

```diff
// key在子节点中需要唯一
<ul>
    <li key="2015">Duke</li>
    <li key="2016">Villanova</li>
</ul>

<ul>
    <li key="2014">Connecticut</li>
    <li key="2015">Duke</li>
    <li key="2016">Villanova</li>
</ul>
// 对比key发现不一样
// 移动key=2015 key=2016
// 插入key=2014
// 减少销毁, 在重新创建的过程
```

## 依赖

- 差异算法不会尝试匹配不同类型的组件树
- `key`应该是稳定并且唯一的, 不稳定的`key`会导致不必要的重新创建

## `virtual dom vs dom`

框架的意义在于简化开发者底层的`DOM`操作,让开发者能声明式些代码, 从而是项目变得更容易维护. 这是一个性能 `vs` 可维护性的取舍.

原生操作 `DOM` 是改变字符串然后 `innerHTML` 插入到文档中. `virtula dom`的基本操作也是如此. 如果发生在大面积的`UI`改变原生操作也没有任何问题, 但是在这个`UI`里面只发生了一行代码变动, 那么`innerHTML`的理念「全部重新渲染」就造成了极大性能浪费.

- `innerHTML`: `render html string O(template size)` + 重新创建所有的 `DOM` 元素`O(DOM size)`
- `virtual dom`: `render virtual DOM` + `diff O(template size)` + 必要的`DOM`更新 `O(DOM change)`

对比起来 `innerHTML` 简单粗暴, 少了`js`对比计算的操作. 但是 `js`的计算是很廉价的. 这样就可以保证 不管 `UI`变化的多与少界面每次的重绘性能都能接受.

### `mvvm vs virtual dom`

`mvvm`变化检查是数据层面的, `react`变化检查是 `DOM`层面的.

`mvvm`采用的 ` Directive/Binding`

- 脏检查: `scope digest O(watcher count)` + 必要 `DOM` 更新 `O(DOM change)`
- 依赖收集: 重新收集依赖 `O(data change)` + 必要 `DOM` 更新 `O(DOM change)`

脏检查最不效率的地方就是在于任何小变动就会检查所有的`watcher`,相反当大量 `watcher` 都变动时, 脏检查优势就出来了.

依赖收集在初始化和数据变化的时候需要重新收集依赖, 如果依赖量少消耗忽略不计, 当数据量庞大消耗就很可观.

`mvvm`在渲染列表的时候初始化几乎一定比 `react` 慢, 因为创建 `viewmodel/scope` 实例昂贵. 关于再次渲染的时候, 在没有做任何复用优化, `mvvm` 都会认为数据都是全新的, `mvvm`会销毁之前的实例, 然后创建新的示例, 再进行渲染. 然而 `react` 只检查 `DOM`结构层面的, 即使是全新的数据, 只要最后渲染结果没有变动, 就不会做无用功.

关于列表重绘的优化机制, `mvvm or virtual`都提供了相似的机制. `angular vue`采用 `track by $index`, `react`采用 `key`.

在性能对比上需要区分场景的, `react`是需要做针对性能优化`shouldComponentUpdate or immutable data`.

- 初始渲染: `virtual DOM` > 脏检查 >= 依赖收集
- 小量数据更新: 依赖收集 >> `virtual DOM` + 优化 > 脏检查(无法优化) > `virtual DOM` 无优化
- 大量数据更新: 脏检查 + 优化 >= 依赖收集 + 优化 > `virtual DOM`(无法/无需优化)>> `MVVM` 无优化

`virtual dom` 带来的并不是性能价值,而是提出了新的概念

- 用函数式编程方式操作 `UI`
- 可以渲染到 `DOM` 以外的 `backend`(`react native`)


# @参考

[Virtual DOM and Internals](https://reactjs.org/docs/faq-internals.html)

[深度剖析: 如何实现一个 Virtual DOM 算法 #13](https://github.com/livoras/blog/issues/13)

[网上都说操作真实 DOM 慢，但测试结果却比 React 更快，为什么？](https://www.zhihu.com/question/31809713)

[React Virtual DOM Diff算法解析](https://sekaiamber.github.io/react-dom-diff/)
