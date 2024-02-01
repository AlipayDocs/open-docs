# 简介

单项选择器组，内部由多个 [`radio`](/mini/component/radio) 组件构成。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/26640e6c0b6e9f35420d563cef47ec7a.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/radio/index&defaultOpenedFiles=pages/radio/index&theme=light)

## 属性说明

| 属性     | 类型        | 描述                                                          |
| -------- | ----------- | ------------------------------------------------------------- |
| onChange | EventHandle | 选中项发生变化时触发，`event.detail = {value: 选中项 radio 的 value}`。 |
| name     | String      | 组件名字，用于表单提交获取数据。                               |
