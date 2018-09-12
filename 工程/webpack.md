# `webpack`

## `entry`

#### 单个入口 `entry: string|Array<string>`

```javascript
// 1
module.exports = {
    entry: './path/to/my/entry/file.js'
};

// 2
module.exports = {
    entry: {
        main: './path/to/my/entry/file.js'
    }
};

//3
module.exports = {
    entry: [
        './path/to/my/entry/file.js',
        './path/to/my/entry/file1.js',
        './path/to/my/entry/file2.js'
    ]
};
```

#### 多页面 `entry: object`

```javascript
module.exports = {
    entry: {
        pageOne: './src/pageOne/index.js',
        pageTwo: './src/pageTwo/index.js',
        pageThree: './src/pageThree/index.js'
    }
};
```

## `output`

无论是单入口还是多入口, 输出只指定一个.

```javascript
output: {
    filename: '[name].js',
    path: __dirname + '/dist'
}
```

## `mode: production|development`

```diff
// mode 的默认值是 production
module.exports = {
+ mode: 'development'
- plugins: [
-   new webpack.NamedModulesPlugin(),
-   new webpack.NamedChunksPlugin(),
-   new webpack.DefinePlugin({ "process.env.NODE_ENV": JSON.stringify("development") }),
- ]
}

// webpack.production.config.js
module.exports = {
+  mode: 'production',
-  plugins: [
-    new UglifyJsPlugin(/* ... */),
-    new webpack.DefinePlugin({ "process.env.NODE_ENV": JSON.stringify("production") }),
-    new webpack.optimize.ModuleConcatenationPlugin(),
-    new webpack.NoEmitOnErrorsPlugin()
-  ]
}

// webpack.custom.config.js
module.exports = {
+  mode: 'none',
-  plugins: [
-  ]
}
```

## `loader`

`loader` 用于对模块的源代码进行转换. `loader` 可以使你在 `import` 或 `load` 模块时预处理文件.

```javascript
// 对于不同的文件使用不同的 loader
module.exports = {
    module: {
        rules: [
            {
                test: /\.css$/,
                use: 'css-loader'
            },
            {
                test: /\.ts$/,
                use: 'ts-loader'
            }
            ...
        ]
    }
};
```

## `plugins`

`plugins` 用于完成 `loader` 无法实现的功能.

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: './path/to/my/entry/file.js',
    output: {
        filename: 'my-first-webpack.bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
        rules: ...
    },
    plugins: [
        new HtmlWebpackPlugin({template: './src/index.html'})
    ]
};
```

## `targets`

主要功能是指定运行环境是什么. 默认是`web`编译为类浏览器环境里可用;

## `HRM` 热更

开发时候让人最舒心的功能.
1. 应用程序代码要求 `HMR runtime` 检查更新
2. `HMR runtime`(异步)下载更新, 然后通知应用程序代码
3. 应用程序代码要求 `HMR runtime` 应用更新
4. `HMR runtime`(异步)应用更新

## `resolve`

模块解析能够解析三种文件路径啊:
- 绝对路径, 已经知道具体位置了不需要做解析
- 相对路径, 是相对上下文目录`(context directory)`会解析成绝对路径
- 模块路径, 模块会根据`resolve-modules`中指定的目录搜索

##### `alias` 设置别名

用于模块引入变得更简单
```javascript
module.exports = {
    //...
    resolve: {
        alias: {
            @Utilities: path.resolve(__dirname, 'src/utilities/')
        }
    }
};
```

```javascript
// before
import Utility from '../../utilities/utility';
// after
import Utility from '@Utilities/utility';
```

[模块解析(`module resolution)`](https://webpack.docschina.org/concepts/module-resolution)

## `optimization`

```javascript
module.exports = {
    // ...
    optimization: {
        minimize: true, // 开启压缩
        nodeEnv: 'production', // 设置环境变量
        sideEffects: true, // 优化代码块副作用
        concatenateModules: true, // 模块作用提升
        splitChunks: { // 代码分割
            chunks: 'all',
        },
        runtimeChunk: true, // 运行时
    },
}
```

[`webpack-4-code-splitting-chunk-graph-and-the-splitchunks-optimization`](https://medium.com/webpack/webpack-4-code-splitting-chunk-graph-and-the-splitchunks-optimization-be739a861366)

[`side-effects`](https://github.com/webpack/webpack/tree/master/examples/side-effects)

[`webpack-4-mode-and-optimization`](https://medium.com/webpack/webpack-4-mode-and-optimization-5423a6bc597a)

[`webpack 打包优化 #5`](https://github.com/evanhunt/blog/issues/5)

## `externals`

防止将从外部引入第三方资源打包到`bundle`中. 而是在`runtime`再去外部获取这些拓展依赖`external dependencies`

```javascript
// html
<script
  src="https://code.jquery.com/jquery-3.1.0.js"
</script>

// webpack.config.js
module.exports = {
    //...
    externals: {
        jquery: 'jQuery'
    }
};

// template
import $ from 'jquery';

$('.my-element').animate(/* ... */);
```

## `DllPlugin`

这个插件是在一个额外的独立的 `webpack` 设置中创建一个只有 `dll` 的 `bundle(dll-only-bundle)`. 这个插件会生成一个名为 `manifest.json` 的文件, 这个文件是用来让 `DLLReferencePlugin` 映射到相关的依赖上去的.

其目的是建立文件的映射关系, 减少文件解析过程来提升`webpack`构建速度.

[`DllPlugin`](https://webpack.docschina.org/plugins/dll-plugin/#src/components/Sidebar/Sidebar.jsx)

## 升级

### `webpack4`

- `mode`
- ~~`CommonsChunkPlugin`~~
- `optimize.splitChunks`

### `webpack3`

- `Scope Hoisting`

### `webpack2`

- `ES6 modules`
- `Tree Shaking`
