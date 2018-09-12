# @`font-face`

`font-face` 是 `CSS3` 中一个新的功能,它可以使自定义字体嵌入到网页中;

## 使用

```css
/* 定义字体 */
@font-face {
    font-family: 'YourWebFontName';
    src: url('YourWebFontName.eot'); /* IE9 Compat Modes */
    src: url('YourWebFontName.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
        url('YourWebFontName.woff') format('woff'), /* Modern Browsers */
        url('YourWebFontName.ttf')  format('truetype'), /* Safari, Android, iOS */
        url('YourWebFontName.svg#YourWebFontName') format('svg'); /* Legacy iOS */
}

/* 使用 */
h2 {
    font-family: 'YourWebFontName'
}
```

### `TureTpe(.ttf)` 格式

`.ttf` 字体是 `Windows` 和 `Mac` 的最常见的字体,是一种 `RAW` 格式,因此他不为网站优化,支持这种字体的浏览器有 `『IE9+,Firefox3.5+,Chrome4+,Safari3+,Opera10+,iOS Mobile Safari4.2+』`

### `OpenType(.otf)` 格式

 `.otf` 字体被认为是一种原始的字体格式,其内置在 `TureType` 的基础上,所以也提供了更多的功能,支持这种字体的浏览器有` 『Firefox3.5+,Chrome4.0+,Safari3.1+,Opera10.0+,iOS Mobile Safari4.2+』`

### `Web Open Font Format(.woff)` 格式
`.woff` 字体是 `Web` 字体中最佳格式,他是一个开放的 `TrueType/OpenType` 的压缩版本,同时也支持元数据包的分离,支持这种字体的浏览器有`『IE9+,Firefox3.5+,Chrome6+,Safari3.6+,Opera11.1+』`

### `Embedded Open Type(.eot)` 格式

`.eot` 字体是 `IE` 专用字体,可以从 `TrueType` 创建此格式字体,支持这种字体的浏览器有 `『IE4+』`

### `SVG(.svg)` 格式

`.svg` 字体是基于 `SVG` 字体渲染的一种格式,支持这种字体的浏览器有 `『Chrome4+,Safari3.1+,Opera10.0+,iOS Mobile Safari3.2+』`

# @参考

[Webfont生成器](https://www.fontsquirrel.com/tools/webfont-generator)
