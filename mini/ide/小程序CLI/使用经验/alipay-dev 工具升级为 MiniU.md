# alipay-dev 品牌升级到 MiniU

alipay-dev 品牌升级到 MiniU，原有用法 **100% 兼容**。

# 升级方式

重新安装 alipay-dev，即升级完成。

```shell
npm install alipay-dev
```

#### 检查是否升级成功

通过查看版本号，只要是 0.5.5，或者 1.x 的就是升级成功。如果使用命令行，可输入：

```shell
alipaydev -v
miniu@1.4.0
```

这样表示已经品牌升级为最新。

# FAQ

### 为什么升级

alipay-dev 在 0.5.4 版本已经很久了，升级后修改了很多之前的 bug，新增了很多功能，部分升级：

- 提升上传文件大小限制；
- 添加请求报错打印日志；
- 添加本地编译功能；
- 添加本地开发功能，像 h5 那样来用 chrome 来开发小程序；
- 添加小程序构建产物及组件分析沟通，分析依赖及组件；
- 添加支付宝小程序转微信小程序功能。

### 是否兼容之前

100% 兼容。

###

# 原有功能使用介绍

升级后原有功能不变，原有用法 100% 兼容。

### 使用命令行

比如查看小程序列表，升级前：

```shell
alipaydev mini list
```

<br />升级后：

```shell
alipaydev mini list
```

###

### 使用 sdk

原有方式：

```shell
const alipaydev = require('alipay-dev');
const miniList = await alipaydev.miniAppList()
```

<br />升级后：

```shell
const alipaydev = require('alipay-dev');
const miniList = await alipaydev.miniAppList()
```

#

# 使用 MiniU

alipay-dev 品牌升级后，推荐使用 MiniU 品牌。

原有安装方式：

```shell
$ npm install alipay-dev
```

升级后：

```shell
$ npm install miniu
```

其他使用方式都不变，包括命令行跟 sdk

### 使用命令行

```shell
miniu mini list
```

### 使用 sdk

```shell
const alipaydev = require('miniu');
const miniList = await alipaydev.miniAppList()
```
