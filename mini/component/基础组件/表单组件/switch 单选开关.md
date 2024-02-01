# 简介

单选开关。

## 使用限制

- iOS 和 Android 展现样式有所差异：iOS 单选开关为圆形，Android 单选开关为方形。
- 不支持自定义 switch 样式，如大小等。

## 扫码体验

![单选开关二维码|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/f5ca37ac5dfd5ae057504beb9ae059e5.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线示例](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/switch/index&defaultOpenedFiles=pages/switch/index&theme=light)

## 属性说明

| **属性** | **类型**   | **描述**                                                               |
| -------- | ---------- | ---------------------------------------------------------------------- |
| name     | String     | 组件名字，用于表单提交获取数据。                                       |
| checked  | Boolean    | 是否选中。                                                             |
| disabled | Boolean    | 是否禁用。                                                             |
| color    | String     | 组件颜色，同 CSS 色值。<br />版本要求：基础库 1.10.0 及以上。            |
| onChange | EventHandle | checked 改变时触发，`event.detail={ value:checked}`。                   |
| controlled | Boolean  | 是否为受控组件，为 true 时，`checked` 会完全受 `setData` 控制。<br />默认值：false<br />版本要求：基础库 1.8.0 及以上。 |
