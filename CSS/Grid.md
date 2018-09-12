# @`Grid`

`CSS Grid Layout` 是 `CSS` 中最强大的布局系统. 它是一个二维系统, 意味着它可以处理列和行(flexbox主要是一维系统). 通过将CSS规则应用于父元素(成为网格容器)和子元素(成为网格项).

## 语法

### `display: grid | inline-grid`

- `grid` 生产块级网格
- `inline-grid` 生产内联网格

下面开始的内容都是 `display: grid` 为基准;

### `grid-template-rows` `grid-template-columns`

定义网格行和列的大小(使用空格分隔定义);

```css
/* Keyword value for example */
grid-template-row
|| grid-template-columns:
[100px] || [10rem] || [10vw] || [10%] || [1fr] || [minmax(100px, 1fr)]

/**
 * 1fr 是自适应大小
 * 2fr 是1/2大小
 * 3fr 是1/3大小
 * 4fr 是1/4大小
 * 5fr 是1/5大小
 * 6fr 是1/6大小
 * ...
 */
```

[jsfiddle demo](https://jsfiddle.net/evan_g/edtnj637/)

### `grid-row` `grid-column`

定义网格元素的大小和跨度区域;

```css
/* 语法 */
grid-row
|| grid-column:
[span] <start> / [span] <end>;
/**
 * [span] 跨度 默认为1;
 * <start> 起始值
 * <end> 结束值
 */
```

[jsfiddle demo](https://jsfiddle.net/evan_g/2xtqf765/)

### `grid-area`

定义网格跨度区域;

```css
/* 语法 */
grid-area: [span] <grid-row-start> /
            [span] <grid-column-start> /
            [span] <grid-row-end> /
            [span] <grid-column-end>
```

[jsfiddle demo](https://jsfiddle.net/evan_g/62w4qd59/)

### `grid-row-gap` `grid-column-gap`

定义行和列的间距;

```css
/* 语法 */
grid-row-gap ||
grid-column-gap: <value> <value> <value> ...
```

## `GRID GARDEN`

一个通过种萝卜来学习 `grid` 布局的小游戏;

[GRID GARDEN
](https://cssgridgarden.com/)

# @参考

[MDN grid](https://developer.mozilla.org/en-US/docs/Web/CSS/grid)
