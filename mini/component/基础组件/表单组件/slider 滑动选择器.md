# 简介

滑动选择器。

# 使用限制
- **Native 渲染引擎**：不支持。可通过 `my.canIUse('slider')` 判断是否支持。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5615dd2ce42f01988e82b704217c14d8.png#align=left&display=inline&height=157&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线体验](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/slider/index&defaultOpenedFiles=pages/slider/index&theme=light)

## 属性说明

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| name | String | 组件名字，用于表单提交时获取数据。 |
| min | Number | 最小值。<br>默认值：0 |
| max | Number | 最大值。<br>默认值：100 |
| step | Number | 步长，需大于 0，并能被（max-min）整除。<br>默认值：1 |
| disabled | Boolean | 是否禁用。<br>默认值：false |
| value | Number | 当前取值。<br>默认值：0 |
| show-value | Boolean | 是否显示当前值。<br>默认值：false |
| active-color | String | 已选择的条颜色，同 CSS 色值。<br>默认值：#108ee9 |
| background-color | String | 背景条颜色，同 CSS 色值。<br>默认值：#ddd |
| track-size | Number | 轨道线条高度。<br>默认值：4 |
| handle-size | Number | 滑块大小。<br>默认值：22 |
| handle-color | String | 滑块填充色，同 CSS 色值。<br>默认值：#fff |
| onChange | EventHandle | 拖动完成后触发的事件，`event.detail = {value: value}`。 |
| onChanging | EventHandle | 拖动过程中触发的事件，`event.detail = {value: value}`。<br>版本要求：基础库 [1.5.0](/mini/framework/compatibility) 及以上。 |
