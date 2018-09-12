# @性能优化原则及分类

## 原则

> 仅供学习参考, 目前很大部分优化手段都已经实现自动化构建

首先, 我们把雅虎14条优化原则, 《高性能网站建设指南》以及《高性能网站建设进阶指南》中提到的优化点做一次梳理, 按照优化方向分类, 可以得到这样一张表格:

| 优化方向 | 优化手段 |
| ------------- |-------------|
| 请求数量 | 合并脚本和样式表, `CSS Sprites`, 拆分初始化负载, 划分主域 |
| 请求带宽 | 开启`GZip`, 精简`JavaScript`, 移除重复脚本, 图像优化 |
| 缓存利用 | 使用`CDN`, 使用外部`JavaScript`和`CSS`, 添加`Expires`头, 减少`DNS`查找, 配置`ETag`, 使`AjaX`可缓存 |
| 页面结构 | 将样式表放在顶部, 将脚本放在底部, 尽早刷新文档的输出 |
| 代码校验 | 避免`CSS`表达式, 避免重定向 |


| 优化方向 | 优化手段 |
| ------------- |-------------|
| 请求数量 | 合并脚本和样式表, 拆分初始化负载 |
| 请求带宽 | 移除重复脚本 |
| 缓存利用 | 添加Expires头, 配置ETag, 使Ajax可缓存 |
| 页面结构 | 将样式表放在顶部, 将脚本放在底部, 尽早刷新文档的输出 |

[阿里无线11.11: 手机淘宝 521 性能优化项目揭秘](http://www.infoq.com/cn/articles/mobile-taobao-521-performance-optimization-project)

## `DNS Prefetching`

`X-DNS-Prefetch-Control` 头控制着浏览器的 `DNS` 预读取功能.  `DNS` 预读取是一项使浏览器主动去执行域名解析的功能, 其范围包括文档的所有链接, 无论是图片的, `CSS` 的, 还是 `JavaScript` 等其他用户能够点击的 `URL`.

因为预读取会在后台执行, 所以 `DNS` 很可能在链接对应的东西出现之前就已经解析完毕. 这能够减少用户点击链接时的延迟.

[DNS 预读取](https://developer.mozilla.org/zh-CN/docs/Controlling_DNS_prefetching)

## 无线优化资料

[无线Web开发经验谈](http://am-team.github.io/amg/dev-exp-doc.html#无线web开发简介)
