# 简介

多选项目。

## 使用限制

Checkbox 不支持修改选中的背景颜色样式。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/os/skylark-tools/public/files/7cff45f9018a7d0a966cfd0f097961b8.jpeg%26originHeight%3D157%26originWidth%3D127%26size%3D20801%26status%3Ddone%26width%3D127#align=left&display=inline&height=157&originHeight=157&originWidth=127&status=done&style=none&width=127)


# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/checkbox/index&defaultOpenedFiles=pages/checkbox/index&theme=light)

## 属性说明

| 属性      | 类型     | 描述                                                  |
| ---------- | --------- | ------------------------------------------------------ |
| value     | String   | 组件值，选中时 change 事件会携带的 value。             |
| checked   | Boolean  | 当前是否选中，可用来设置默认选中。<br />默认值：false   |
| disabled  | Boolean  | 是否禁用。<br />默认值：false                           |
| onChange  | EventHandle | 组件发生改变时触发，detail = {value: 该 checkbox 是否 checked }。 |
| color     | String   | Checkbox 的颜色，同 CSS 色值。<br />版本要求：基础库 [1.10.0](/mini/framework/compatibility) 及以上 |
