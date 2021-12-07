
# 简介
小程序扩展组件库 mini-ali-ui， 由原 mini-antui  组件库升级而来，是 [基础组件库](https://opendocs.alipay.com/mini/component) 的重要补充。mini-ali-ui 是基于 [小程序自定义组件规范](https://opendocs.alipay.com/mini/framework/custom-component-overview) 开发的一套开源 UI 组件库，供小程序开发者快速复用。**mini-antui 目前已停止维护，如需使用原 mini-antui  组件库，请参见 **[**GitHub**](https://github.com/ant-mini-program/mini-antui)**、**[**获取文档**](https://gw.alipayobjects.com/os/bmw-prod/7b918fd1-f610-44a0-9cca-dcb6b513b792.pdf)**，建议使用 mini-ali-ui。**

## 特性

- 基于 Alipay Design 设计规范。
- 支持多端小程序（支付宝，淘宝，钉钉等）。
- 支持主题配置切换。
- 支持 px 与 rpx。

## 安装

- 打开 IDE，进入 **支付宝小程序** > **模板选取** > **入门** > **API-Demo**，右侧模拟器中选择扩展组件。
- IDE 左侧功能面板中选择 **NPM 依赖管理** 添加以下依赖。详情请参见 [NPM 管理](https://opendocs.alipay.com/mini/ide/npm-manage)。
```
$ npm install mini-ali-ui --save
```

# 使用
在页面 json 文件中进行注册，如[ title 标题](https://opendocs.alipay.com/mini/component-ext/title) 组件的注册如下所示：
```
{
  "usingComponents": {
    "title": "mini-ali-ui/es/title/index"
  }
}
```
如安装的是 rpx 版本的 mini-ali-ui，那么在进行组件注册时，修改一下名称即可，方式如下：
```
{
  "usingComponents": {
    "title": "mini-ali-ui-rpx/es/title/index"
  }
}
```
组件注册成功之后，具体的使用方式无差别。

在 AXML 文件中进行调用：
```
<title
  hasLine="true"
  iconURL="https://t.alipayobjects.com/images/T1HHFgXXVeXXXXXXXX.png"
  type="close"
  onActionTap="titleClose"
>内部标题可关闭
</title>
```

## 版本升级
可使用如下命令升级 UI 组件版本（当前最新版本 1.3.0）。
```
$ npm update mini-ali-ui --save
```

# 贡献
如果你有好的意见或建议，欢迎给我们提 [issue](https://github.com/Alibaba-mp/mini-ali-ui/issues)。
