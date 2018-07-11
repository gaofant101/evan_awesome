# @ 使用指南

官网 (https://atom.io/)

## @设置代理

### `window`

```
C:Users\?\.atom\.apmrc配置文件（如果该目录下没有该配置文件：找到位置C:Users\?\.atom\.apm\.apmrc配置文件复制到C:Users\?\.atom目录下并删除内容）

strict-ssl = false
http_proxy = http://127.0.0.1:useport
https_proxy = http://127.0.0.1:useport
```

### `mac`
```
apm config set strict-ssl false
apm config set http-proxy https://127.0.0.1:port
apm config set https-proxy https://127.0.0.1:port

```

### 取消 `APM` 代理

```
Settings > Core > Use Proxy Settings When Calling APM
```

## @ `Atom` 使用

### 插件


- `javascript` 下的 `JavaScript Snippets` `language-javascript-jsx` `es6-javascript`

- `language-babel` 语法支持 ES6、JSX、Flow …，还支持预览 babel 或 react 编译结果

- `react` 下的 `react-snippets` `react-es6-snippets`

- `vue` 下的 `language-vue`

- `Markdown Preview` Markdown语法插件

- `markdown-scroll-sync` markdown文件，右侧实时滚动

- `markdown-writer` 使你更好的书写 markdown 文件

- `emmet`HTML增强

- `autoclose-html` 自动闭合 `html` 标签

- `block-comment` 生成块级注释

- `highlight-line` 当前行高亮

- `highlight-selected` 高亮当前文件中所有匹配的选择文字

- `file-icon` 文件图标

- `filecolor` 文件颜色

- `Atom Material` 主题

- `docblockr` 文档注释

### 设置

#### 设置Tab 为空格

`setting` -> `Editot` -> `Tab Type` 选择 `soft` ;   
`Tab length` 设置indent 为 `4`

#### 设置字体和字号

`file` -> `Stylesheet` ->

```css
/*
 * Your Stylesheet
 *
 * This stylesheet is loaded when Atom starts up and is reloaded automatically
 * when it is changed and saved.
 *
 * Add your own CSS or Less to fully customize Atom.
 * If you are unfamiliar with Less, you can read more about it here:
 * http://lesscss.org
 */


/*
 * Examples
 * (To see them, uncomment and save)
 */

// style the background color of the tree view
.tree-view {
    // background-color: whitesmoke;
    font-size: 14px;
    font-family: Courier New;
}

// style the background and foreground colors on the atom-text-editor-element itself
atom-text-editor {
    // color: white;
    // background-color: hsl(180, 24%, 12%);
    font-size: 17px;
    font-family: Courier New;
}

// style UI elements inside atom-text-editor
atom-text-editor .cursor {
    // border-color: red;
}

```

# @ `issues`

Atom 1.28 crashes on macOS with Shadowsocks proxy (https://github.com/atom/atom/issues/17557)
