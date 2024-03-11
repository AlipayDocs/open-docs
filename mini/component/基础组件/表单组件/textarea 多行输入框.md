# 简介

多行输入框，可输入多行内容。支持使用 [my.hideKeyboard](https://opendocs.alipay.com/mini/api/ui-hidekeyboard) 接口隐藏输入键盘。你可以在 [input](https://opendocs.alipay.com/mini/component/input) 组件中加上 `enableNative="{{false}}"`，避免 `textarea` 弹出键盘后出现内容上移。在 `textarea` 代码中加上 `enableNative="{{false}}"`，可解决 Android 系统下 `textarea` 获取焦点的时候文字消失问题。

## 使用限制

- **Native 渲染引擎**：暂不支持。你可以通过 `my.canIUse('textarea')` 判断是否支持此功能。
- 不支持通过 `textarea` 获取键盘高度。
- 不支持 iOS 系统支付宝客户端版本 10.1.80 及以上使用 `focus=true` 自动唤起。
- 添加属性 `controlled="{{true}}"` 表示 `value` 内容会完全受 `setData` 控制。
- `confirm-type` 与 `enableNative` 属性冲突，若希望 `confirm-type` 生效，`enableNative` 不能设定为 `false`。

## 扫码体验

![](https://gw.alipayobjects.com/zos/skylark/3e5f83dd-fcbe-43d6-9466-7259f98723c6/2018/jpeg/eab73793-ef6e-4a7c-b347-0044244a6ae1.jpeg)

# 使用

## 在线示例

请访问 [小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/textarea/index&defaultOpenedFiles=pages/textarea/index&theme=light) 查看示例。

## 属性说明

| 属性 | 类型 | 描述 |
| ------ | ------ | ------ |
| name | String | 组件名字，用于表单提交获取数据。 |
| value | String | 初始内容。 |
| placeholder | String | 占位符。 |
| placeholder-style | String | 指定 `placeholder` 的样式。<br />**版本要求**：基础库 [1.6.0](/mini/framework/compatibility) 及以上 |
| placeholder-class | String | 指定 `placeholder` 的样式类。<br />**版本要求**：基础库 [1.6.0](/mini/framework/compatibility) 及以上 |
| disabled | Boolean | 是否禁用。<br />**默认值**：`false` |
| maxlength | Number | 最大长度，当设置为 `-1` 时不限制最大长度。<br />**默认值**：`140` |
| focus | Boolean | 获得焦点。<br />**默认值**：`false` |
| auto-height | Boolean | 是否自动增高。<br />**默认值**：`false` |
| show-count | Boolean | 是否渲染字数统计功能。<br />**默认值**：`true`<br />**版本要求**：基础库 [1.8.0](/mini/framework/compatibility) 及以上 |
| controlled | Boolean | 是否为受控组件。设为 `true` 时，`value` 内容会完全受 `setData` 控制。<br />**默认值**：`false`<br />**版本要求**：基础库 [1.8.0](/mini/framework/compatibility) 及以上 |
| confirm-type | String | 设置键盘右下角按钮的文字。有效值：`return`（显示“换行”）、`done`（显示“完成”）、`go`（显示“前往”）、`next`（显示“下一个”）、`search`（显示“搜索”）、`send`（显示“发送”）。<br />**注意**：仅支持 Android。<br />**默认值**：`return`。<br />**版本要求**：基础库 [2.7.23](https://opendocs.alipay.com/mini/ide/framework-changelog-v2) 及以上、支付宝客户端 10.2.80 及以上 |
| onInput | EventHandle | 键盘输入时触发，`event.detail = {value: value, cursor: cursor}`。<br />**版本要求**：字段 `cursor` 基础库 [1.17.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上开始支持。 |
| onFocus | EventHandle | 输入框聚焦时触发，`event.detail = {value: value}`。 |
| onBlur | EventHandle | 输入框失去焦点时触发，`event.detail = {value: value}`。 |
| onConfirm | EventHandle | 点击完成时触发，`event.detail = {value: value}`。 |
