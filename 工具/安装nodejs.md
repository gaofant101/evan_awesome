## @ 下载node

[官网](https://nodejs.org/zh-cn/download/)


### 检测有没有安装成功

```shell
node -v
npm -v
```

```shell
# 修改源地址为淘宝 NPM 镜像
npm config set registry http://registry.npm.taobao.org/

# 修改源地址为官方源
npm config set registry https://registry.npmjs.org/
```

### 指定文件 `[node_modules]` 安装路径

在你安装 `NODE` 的根目录下创建 `node_global` `node_cache` 2个文件夹

创建完过后使用命令修改配置(这了我默认安装到`D:`盘)
```shell
npm config set prefix "D:\NODE\node_global"
npm config set cache "D:\NODE\node_cache"
```

在`我的电脑`进入`高级配置`->`环境变量`->新建`NODE_PATH`->输入`D:\NODE\node_global\node_modules`

在用户变量下的`path`中的`NODE`环境变量修改为->`D:\NODE\node_global`
