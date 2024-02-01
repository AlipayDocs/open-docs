# 简介

单选按钮。

## 使用限制

- 不支持修改 radio 选中后的宽高。
- 不支持 radio 按钮与 [text](https://opendocs.alipay.com/mini/component/text) 标签嵌套，支持平行关系。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/4b07417d74a2578ab1d5da6b5965507a.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/radio/index&defaultOpenedFiles=pages/radio/index&theme=light)

## 属性说明

| **属性**    | **类型**    | **描述**                                                        |
|-------------|-------------|-----------------------------------------------------------------|
| value       | String      | 组件值，选中时 change 事件会携带的 value。                     |
| checked     | Boolean     | 当前是否选中。<br />**默认值：** false                          |
| disabled    | Boolean     | 是否禁用。<br />**默认值：** false                              |
| color       | String      | radio 的颜色，同 CSS 色值。<br />**版本要求：**基础库 1.10.0 及以上 |
