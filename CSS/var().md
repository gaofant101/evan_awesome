# @`CSS`变量

在构建大型站点时, 太多的模块会导致`css`难以维护; 例如大量样式规则会重复使用、网站的配色方案对于颜色的定义也是重复规则;

`LESS` & `SASS` 处理器的变量、嵌套等功能对`css`有极大的帮助;

`css` 也引入层级变量的概念, 使得`css`也能自定义变量;

> var() 只有目前比较新的浏览器版本才支持;   
> 查看兼容表 https://caniuse.com/#search=var

## 语法

```css
/* 定义一个简单的theme */
:root{
    --border-width:1px;
    --border-style:solid;
    --border-theme: #ff7a45;
    --background-theme: #ffd8bf;
    --color-theme: #ff7a45;
}

/* ... 省略布局 */

.sidle{
    background: var(--background-theme);
    border: var(--border-width) var(--border-style) var(--border-theme);
    color: var(--color-theme);
}
.head{
    border: var(--border-width) var(--border-style) var(--border-theme);
    color: var(--color-theme);
}
.content{
    border: var(--border-width) var(--border-style) var(--border-theme);
}
```

[var() jsfiddle demo](https://jsfiddle.net/evan_g/76uhmr9g/)

# @参考

[MDN 使用CSS变量
](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Using_CSS_variables)
