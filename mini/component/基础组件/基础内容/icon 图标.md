# 简介

图标。

## 使用限制

- `icon` 组件不支持 `onTap`、`catchTap` 等点击事件。
- 跳转页面后左上角显示返回上一页 `icon`，不支持隐藏。
- `icon` 中所应用的样式如果是插件中的样式，建议修改样式定义的 `class` 名等信息，否则 `icon` 中不写插件代码显示正常，添加插件代码 `icon` 显示不正常。

## 扫码体验

![图标体验二维码](https://gw.alipayobjects.com/zos/skylark-tools/public/files/7380714f62c709478a9a507f9ff8450d.png)

# 使用

## 在线示例

[小程序在线示例](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/icon/index&defaultOpenedFiles=pages/icon/index&theme=light)

## 属性说明

| 属性 | 类型   | 描述                                                       |
| ---- | ------ | ---------------------------------------------------------- |
| type | String | `icon` 类型。有效值：`info`、`warn`、`waiting`、`cancel`、`download`、`search`、`clear`、`success`、`success_no_circle`、`loading`。<br />版本要求：`loading` 支持基础库 1.7.2 及以上版本。 |
| size | Number | `icon` 大小，单位为 px。<br />默认值：23                    |
| color| String | `icon` 颜色，同 CSS 色值。                                  |
