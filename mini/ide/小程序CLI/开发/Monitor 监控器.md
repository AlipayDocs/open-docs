
# Monitor 面板
很多情况下，开发者需要查看网络情况与 JSAPI 调用的时序情况，Monitor 将小程序的网络请求` my.request` 以及其他 [小程序前端API](https://opendocs.alipay.com/mini/api) 比如 `my.getLocation` 都进行了监控。开发者可以很方便的在一个面板里查看其调用的时序、状态、请求值、返回值、大小及耗时。

![|723x484](https://cdn.nlark.com/yuque/0/2021/png/179989/1618215129592-42f11c37-5d35-43f9-8eee-eec0a10416f3.png#align=left&display=inline&height=894&margin=%5Bobject%20Object%5D&name=image.png&originHeight=894&originWidth=1336&size=476049&status=done&style=none&width=1336)

![|723x484](https://cdn.nlark.com/yuque/0/2021/png/179989/1618215163410-c95e64f7-95c3-4237-b7dd-4d8e33fcc780.png#align=left&display=inline&height=1788&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1788&originWidth=2672&size=679171&status=done&style=none&width=2672)

如上图，被 mock 的 JSAPI 或 HTTP请求，在 Monitor 面板中会展示mock 标志，方便查看。


## Monitor 展示内容
Monitor 会有三种类型的展示：

- Request 调用` my.request `的请求；
- JSAPI 调用其他 `my.xx` 的方法，比如 `my.alert`, `my.getLocation `等；

所有的类型都是按照发起的时间顺序排列，包括了 “Name”，“Status”， “Type”，“Time”，“Size” 几个维度。


# 本地Mock面板
点击勾选“Mock面板”，打开本地mock功能的控制面板。如下图：

![|723x484](https://cdn.nlark.com/yuque/0/2021/png/179989/1618215230770-7ca79ccf-2ade-41ee-9067-da8eb049e47d.png#align=left&display=inline&height=1788&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1788&originWidth=2672&size=634696&status=done&style=none&width=2672)

## 创建mock
创建mock有三种方式， 如下图：

![|723x484](https://cdn.nlark.com/yuque/0/2021/png/179989/1618215251639-79c9076c-698a-441d-9067-8b7276dfc2b2.png#align=left&display=inline&height=1788&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1788&originWidth=2672&size=641531&status=done&style=none&width=2672)

1. 选中monitor条目，打开请求详情面板，详情面板上有“创建mock”按钮，点击按钮创建基于当前请求返回数据的mock；
1. 双击monitor条目，也会基于当前请求和返回数据创建mock；
1. 在Mock面板上，有“新增”按钮，创建mock；

![|723x484](https://cdn.nlark.com/yuque/0/2021/png/179989/1618215286297-594ee4d8-d268-4849-bc24-f762c91b933e.png#align=left&display=inline&height=894&margin=%5Bobject%20Object%5D&name=image.png&originHeight=894&originWidth=1336&size=396806&status=done&style=none&width=1336)

## Mock展示内容

1. “启用”开关，mock功能的启用和关闭；
1. 下图中，“2”位置，单条mock的的启用或关闭；
1. 编辑mock返回内容，直接修改mock数据，实时生效。

![|723x484](https://cdn.nlark.com/yuque/0/2021/png/179989/1618215325658-e038c630-cccd-4abf-89f8-edeb48170010.png#align=left&display=inline&height=1788&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1788&originWidth=2672&size=733806&status=done&style=none&width=2672)
