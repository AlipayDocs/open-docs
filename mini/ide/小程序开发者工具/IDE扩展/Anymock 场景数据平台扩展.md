## 公告
Anymock 产品预计于 2023-12-30 后下线，请在此前完成数据和服务的迁移，感谢您对产品的支持。
## 简介

[Anymock](https://anymock.alipay.com/) 是一个高效、易用的数据接口平台，旨在为开发、测试、设计人员提供功能强大的接口 Mock 及接口管理服务。 Anymock [小程序开发者工具](https://opendocs.alipay.com/mini/ide/download)（简称 IDE）扩展，为 IDE 提供了 mock 任意一个 JSAPI 的能力。同时，支付宝提供了真机预览的 mock 能力，即小程序在真机上预览时也可以使用 Anymock 的 mock 数据。

## 安装 Anymock 扩展

### 1. 下载小程序开发者工具

下载并安装 小程序开发者工具（简称 IDE）。

### 2. 安装 Anymock 扩展

打开小程序开发者工具，打开一个支付宝小程序进入编辑器窗口，在左侧工具栏点击扩展市场图标，搜索 Anymock，进行安装。 ![](https://cdn.nlark.com/yuque/0/2022/png/179989/1651026977812-6284aa71-d618-460e-b4d9-a2947d985217.png)

## 使用 Anymock 扩展

### 1. 启用 Anymock

安装 Anymock 扩展之后可以在侧边菜单栏发现 Anymock 的入口图标，点击图标打开配置面板，打开 **开启 Anymock** 开关。 ![](https://cdn.nlark.com/yuque/0/2022/png/179989/1651027114271-5e979e2e-1c86-4d25-94c6-e2243fc4d6b8.png)

在小程序 Lite 模式下，Anymock 的入口在项目配置菜单内。 ![|284x549](https://cdn.nlark.com/yuque/0/2022/png/179989/1651026997092-98c48fea-952e-4631-9ad5-900081bfd1ec.png)![|284x549](https://cdn.nlark.com/yuque/0/2022/png/179989/1651027001262-fc076db3-b20b-47b1-a744-ceb7dd4d0a93.png)

### 2. 设置项目 Token

Anymock 功能使用依赖于项目 Token（**注意请勿泄露给他人**）。在 Anymock 平台的项目列表中可直接点击复制项目 Token，并粘贴到上图扩展配置页面的 **项目 Token** 一项中。也可以在 Anymock 平台的项目 Workspace 进行项目 Token 的查看、复制和重置。 ![](https://cdn.nlark.com/yuque/0/2022/png/179989/1651027007986-5e4f8163-36a7-4978-9688-0c31143f211a.png)

## Anymock 快速上手

### 1. 新建项目

![](https://cdn.nlark.com/yuque/0/2022/gif/179989/1651027012569-74c605a5-21ff-4eca-85b2-f6f40ec60751.gif)

### 2. 项目 workspace 介绍

可以在 Anymock 平台上创建项目/接口/数据，小程序 IDE 里就可以直接消费了。关于 Anymock 平台能力请查看 [官方文档](https://www.yuque.com/anymock/docs)。 ![](https://cdn.nlark.com/yuque/0/2022/gif/179989/1651027018113-46dba4d8-9177-40af-88e7-c40be563fa02.gif)

### 3. 使用 mock 数据

在使用 IDE 开发小程序过程中，代码层面不需要做任何感知就可以使用 Anymock，可以在 DevTool 里看到打印的 Anymock 日志。Anymock 平台中的数据支持函数编程、MockJs 等特性，方便开发者使用，详情请查看 [官方文档](https://www.yuque.com/anymock/docs/mockdata)。

**注意**：没有命中 mock 数据的接口，会自动走原生链路返回。

在 Anymock 平台编写 mock 数据 ![](https://cdn.nlark.com/yuque/0/2022/png/179989/1651027020529-e6f083b6-ca52-4cfc-8d0e-1453465ea0cd.png)

在项目里调用 my.request 接口，会得到 Anymock 对应接口的返回值。

```javascript
my.request({
  url: 'http://httpbin.org/get',
  method: 'GET',
  data: {
    from: '支付宝',
    name: '支小宝',
  },
  dataType: 'json',
  complete: function (res) {
    console.log('complete:', res);
    my.alert({ content: JSON.stringify(res) });
  },
});
```

比如之前的返回值是：

```javascript
{
  "success": true,
  "name": "Hi HTTP GET"
}
```

在调试器里可看到对应的返回值： ![](https://cdn.nlark.com/yuque/0/2022/png/179989/1651027024646-e353ee07-d77c-44d4-a49b-4c361f7d4b3e.png) 在 Anymock 里修改这个返回值，请求的响应就会修改。

## 其它

Anymock 的初衷是让开发者无感知地使用 Mock 数据，所以为[小程序开发者工具](https://www.yuque.com/anymock/docs/ide)、[Google Chrome](https://www.yuque.com/anymock/docs/chrome) 等提供了官方插件，开发者在这些研发环境下无需做任何代码改动，就可以轻松使用 Anymock 提供的服务。

## 反馈

- [Anymock 官方网站](https://anymock.alipay.com/)
- [Anymock 官方文档](https://www.yuque.com/anymock/docs)
- [Anymock 官方讨论区](https://www.yuque.com/anymock/topics)
