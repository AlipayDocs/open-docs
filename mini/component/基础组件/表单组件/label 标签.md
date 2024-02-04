# 简介

用于提高表单组件的可用性。使用 `for` 属性找到对应组件的 ID，或者将组件放在该标签下。当点击时，就会聚焦对应的组件。`for` 优先级高于内部组件，内部有多个组件时，默认触发第一个组件。

## 使用限制

`label` 标签不支持 `onTap`、`catchTap` 等点击事件。目前可以绑定的组件有：[`checkbox`](https://opendocs.alipay.com/mini/component/checkbox)、[`radio`](https://opendocs.alipay.com/mini/component/radio)、[`input`](https://opendocs.alipay.com/mini/component/input)、[`textarea`](https://opendocs.alipay.com/mini/component/textarea)。

## 扫码体验

![](https://cdn.nlark.com/yuque/0/2022/jpeg/179989/1658114324014-567c0368-16c4-4dda-a286-c2e3fd12ddbc.jpeg)

# 使用

## 在线示例

[小程序在线示例](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/label/index&defaultOpenedFiles=pages/label/index&theme=light)

## 属性说明

| 属性 | 类型   | 描述               |
| ---- | ------ | ------------------ |
| for  | String | 绑定的组件 ID。    |
