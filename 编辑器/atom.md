### 使用指南

[下载地址](https://atom.io/)


##### 设置代理

window环境下

`C:Users\?\.atom\.apmrc`配置文件（如果该目录下没有该配置文件：找到位置`C:Users\?\.atom\.apm\.apmrc`配置文件复制到`C:Users\?\.atom`目录下并删除内容）。

1.用淘宝的源

    registry=https://registry.npm.taobao.org/
    strict-ssl=false

2.用自己的代理端口

    strict-ssl = false
    http_proxy = http://127.0.0.1:useport
    https_proxy = http://127.0.0.1:useport

Mac 环境下

    apm config set strict-ssl false
    apm config set http-proxy https://127.0.0.1:port
    apm config set https-proxy https://127.0.0.1:port

##### 检查安装下载Node、Python、Visual Studio

检查自己本地环境有没有安装`Node`、`Python`、`Visual Studio`环境

[Python 下载地址](https://www.python.org/downloads/)
[Node 下载地址](https://nodejs.org)

`windows`下设置环境变量
`右键我的电脑` -> `高级系统设置` -> `环境变量` -> `系统变量` -> `path` -> `新建` -> `你的安装目录:\Python\`

命令行中输入`python`如果显示

    Python 2.7.13 (v2.7.13:a06454b1afa1, Dec 17 2016, 20:42:59) [MSC v.1500 32 bit (Intel)] on win32
    Type "help", "copyright", "credits" or "license" for more information.
    >>>

就表示安装成功




