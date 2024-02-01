# 简介

[`movable-view`](https://opendocs.alipay.com/mini/component/movable-view) 的可移动区域。

## 使用限制

- 版本要求基础库 1.11.0 或更高版本；若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- **Native 渲染引擎**：暂不支持。可以通过 `my.canIUse('movable-area')` 判断是否支持。
- 必须设置 `width` 和 `height` 属性，不设置则默认为 `10px`。

## 扫码体验

![](https://gw.alipayobjects.com/mdn/rms_d929c6/afts/img/A*V9IxRbitTwkAAAAAAAAAAABjARQnAQ)

# 使用

## 在线示例

[小程序在线示例](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/movable-view/index&defaultOpenedFiles=pages/movable-view/index&theme=light)

## 属性说明

| 属性 | 类型 | 必填 | 描述 |
| --- | --- | --- | --- |
| scale-area | Boolean | 否 | 当里面的 `movable-view` 设置为支持双指缩放时，设置此值可将缩放手势生效区域修改为整个 `movable-area`。<br>**默认值**：`false`<br>**版本要求**：基础库 1.20.0 及以上 |
