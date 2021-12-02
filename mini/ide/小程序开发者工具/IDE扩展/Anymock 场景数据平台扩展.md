
## 简介
[Anymock](https://anymock.alipay.com/) 是一个高效、易用的数据接口平台，旨在为开发、测试、设计同学提供功能强大的接口 Mock 及接口管理服务。

Anymock [小程序开发者工具](https://opendocs.alipay.com/mini/ide/download)（简称 IDE）扩展，为 IDE 提供了 mock 任意一个 JSAPI 的能力。同时，支付宝提供了真机预览的 mock 能力，即小程序在真机上预览时也可以使用 Anymock 的 mock 数据。

## 安装 Anymock 扩展

### 1. 下载小程序开发者工具
下载并安装 [小程序开发者工具](https://opendocs.alipay.com/mini/ide/download)（简称 IDE）。

### 2. 安装 Anymock 扩展
打开小程序开发者工具，打开一个支付宝小程序进入编辑器窗口，在左侧工具栏点击扩展市场图标，搜索 Anymock，进行安装。
![|723x452](https://mdn.alipayobjects.com/afts/img/A*Y8JLQZxlHVkAAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=0H78hyTb_YJaWseDI7haPgAAAABkMK8AAAAA#align=left&display=inline&height=640&margin=%5Bobject%20Object%5D&originHeight=640&originWidth=1024&status=done&style=none&width=1024)

## 使用 Anymock 扩展

### 1. 启用 Anymock
安装 Anymock 扩展之后可以在侧边菜单栏发现 Anymock 的入口图标，点击图标打开配置面板，打开 **开启 Anymock** 开关。

![|723x434](https://mdn.alipayobjects.com/afts/img/A*ZuMGRZD2MW4AAAAAAAAAAAAAAa8wAA/original?bz=openpt_doc&t=XBFliQB4OGHFteiP0vofaAAAAABkMK8AAAAA#align=left&display=inline&height=615&margin=%5Bobject%20Object%5D&originHeight=1862&originWidth=3102&status=done&style=none&width=1024)

在小程序 Lite 模式下，Anymock 的入口在项目配置菜单内。

![|284x549](https://cdn.nlark.com/yuque/0/2021/png/179989/1622775535434-bc9c3f88-8bcb-4484-99e2-1c6b3512404b.png#align=left&display=inline&height=549&margin=%5Bobject%20Object%5D&name=image.png&originHeight=2126&originWidth=1100&size=971333&status=done&style=none&width=284)![|284x547](https://cdn.nlark.com/yuque/0/2021/png/179989/1622775553355-f94d4c55-02c8-4899-8605-7b9c2bb0e493.png#align=left&display=inline&height=547&margin=%5Bobject%20Object%5D&name=image.png&originHeight=2184&originWidth=1134&size=989549&status=done&style=none&width=284)

### 2. 设置项目 Token
Anymock 功能使用依赖于项目 Token（**注意请勿泄露给他人**）。在 Anymock 平台的项目列表中可直接点击复制项目 Token，并粘贴到上图扩展配置页面的 **项目 Token** 一项中。也可以在 Anymock 平台的项目 Workspace 进行项目 Token 的查看、复制和重置。
![|723x196](https://mdn.alipayobjects.com/afts/img/A*xj2ZRaPkg90AAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=3i8rEtq0j07G_r6WMlXJtQAAAABkMK8AAAAA#align=left&display=inline&height=278&margin=%5Bobject%20Object%5D&originHeight=278&originWidth=1024&status=done&style=none&width=1024)

## Anymock 快速上手

### 1. 新建项目
![|723x415](https://mdn.alipayobjects.com/afts/img/A*uit9RpsHvwRBYy5HkRmSDwBkAa8wAA/1024w_1024h_1l.gif?bz=openpt_doc&t=ZjQlhqbr8INKJLDiRybPVQAAAABkMK8AAAAA#align=left&display=inline&height=588&margin=%5Bobject%20Object%5D&originHeight=588&originWidth=1024&status=done&style=none&width=1024)

### 2. 项目 workspace 介绍
可以在 Anymock 平台上创建项目/接口/数据，小程序 IDE 里就可以直接消费了。关于 Anymock 平台能力请参考 [官方文档](https://www.yuque.com/anymock/docs)。

![|723x415](https://mdn.alipayobjects.com/afts/img/A*F0UAQLrZg6N_4dZOjiZaJABkAa8wAA/1024w_1024h_1l.gif?bz=openpt_doc&t=I79LbmDdJVPvLuIZMiQBzwAAAABkMK8AAAAA#align=left&display=inline&height=588&margin=%5Bobject%20Object%5D&originHeight=818&originWidth=1425&status=done&style=none&width=1024)

### 3. 使用 mock 数据
在使用 IDE 开发小程序过程中，代码层面不需要做任何感知就可以使用 Anymock，可以在 DevTool 里看到打印的 Anymock 日志。Anymock 平台中的数据支持函数编程、MockJs等特性，方便开发者使用，详情请参考 [官方文档](https://www.yuque.com/anymock/docs/mockdata)。

**注意**：没有命中 mock 数据的接口，会自动走原生链路返回。

在 Anymock 平台编写 mock 数据

![|723x503](https://mdn.alipayobjects.com/afts/img/A*PMQ4SaklpR4AAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=e1e2WNDIagpJePO0w74TWgAAAABkMK8AAAAA#align=left&display=inline&height=712&margin=%5Bobject%20Object%5D&originHeight=712&originWidth=1024&status=done&style=none&width=1024)

在项目里调用 my.request 接口，会得到 Anymock 对应接口的返回值
```javascript
my.request({
   url: 'http://httpbin.org/get',
   method: 'GET',
   data: {
     from: '支付宝',
     name: '支小宝',
   },
   dataType: 'json',
   complete: function(res) {
     console.log('complete:', res);
     my.alert({ content: JSON.stringify(res)});
   }
 });
```
比如之前的返回值是：
```javascript
{
  "success": true,
  "name": "Hi HTTP GET"
}
```
在调试器里可看到对应的返回值：

![|723x452](https://mdn.alipayobjects.com/afts/img/A*ei_bT4MaAmUAAAAAAAAAAABkAa8wAA/1024w_1024h_1l.png?bz=openpt_doc&t=tUI9Y8__-k8m3lHIBmsiHAAAAABkMK8AAAAA#align=left&display=inline&height=640&margin=%5Bobject%20Object%5D&originHeight=640&originWidth=1024&status=done&style=none&width=1024)

在 Anymock 里修改这个返回值，请求的响应就会修改。

## 其他
Anymock 的初衷是让开发者无感知地使用 Mock 数据，所以为[ 小程序开发者工具](https://www.yuque.com/anymock/docs/ide)、[Google Chrome](https://www.yuque.com/anymock/docs/chrome) 等提供了官方插件，开发者在这些研发环境下无需做任何代码改动，就可以轻松使用 Anymock 提供的服务。

## 反馈

- [Anymock 官方网站](https://anymock.alipay.com/)
- [Anymock 官方文档](https://www.yuque.com/anymock/docs)
- [Anymock 官方讨论区](https://www.yuque.com/anymock/topics)
- Anymock 官方答疑钉钉群：

![|354x400](https://cdn.nlark.com/yuque/0/2021/jpeg/179989/1625552980703-ea52eea2-b3dd-4cbd-abc8-ec69954abfd4.jpeg#align=left&display=inline&height=400&margin=%5Bobject%20Object%5D&name=original%20%283%29.jpg&originHeight=400&originWidth=354&size=65908&status=done&style=none&width=354)
