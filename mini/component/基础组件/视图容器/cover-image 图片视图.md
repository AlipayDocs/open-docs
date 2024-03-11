# 简介

覆盖在原生组件之上的图片视图，可覆盖的原生组件同 [cover-view](https://opendocs.alipay.com/mini/component/cover-view) 一致。

## 使用限制

- **版本要求：** 基础库 1.10.0 及以上，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- **Native 渲染引擎**：暂不支持。可以通过 `my.canIUse('cover-image')` 判断是否支持。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/mdn/rms_d929c6/afts/img/A*JFj2RaJ7iKEAAAAAAAAAAABjARQnAQ#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/cover-view/index&defaultOpenedFiles=pages/cover-view/index&theme=light)

## 属性说明

| 属性 | 类型   | 描述                                                         |
| ---- | ------ | ------------------------------------------------------------ |
| src  | String | 图片地址，支持的地址格式同 `image` 组件一致。<br />**版本要求：** 基础库 1.9.0 及以上 |
| onTap | EventHandle | 点击事件回调。<br />**版本要求：** 基础库 1.9.0 及以上       |
