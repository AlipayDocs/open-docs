# 简介

嵌入页面的滚动选择器。 其中只可放置 picker-view-column 组件，其它节点不会显示。如需获取数组中值，可以先获取索引 index 然后通过 index 再获取数组中值。

## 使用限制

- 该组件内部请勿放入 hidden 或 display none 的节点，需要隐藏请用 a:if 切换。
- 不支持背景色设置成透明，可以修改颜色。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/d93b902d444664bdadf2b4a7c7e6ba4b.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/picker-view/index&defaultOpenedFiles=pages/picker-view/index&theme=light)

## picker-view-column 滚动选择器子项

滚动选择器子项。仅可放置于 picker-view 中，其孩子节点的高度会自动设置成与 picker-view 的选中框的高度一致。<br />**说明：** 该组件内部请勿放入 hidden 或 display none 的节点，需要隐藏请用 `a:if` 切换，即： <br /><br />推荐示例：<br />

```html
<view a:if="{{xx}}"><picker-view /></view>
```

错误示例：

```html
<view hidden="{{xx}}"><picker-view /></view>
```

## picker-view 属性

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| value | Number Array | 数组中的数字表示 picker-view-column 中对应的 index （从 0 开始）。<br />示例：`value=“{{[2]}}”` |
| indicator-style | String | 选中框样式。 |
| indicator-class | String | 选中框的类名。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| mask-style | String | 蒙层的样式。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| mask-class | String | 蒙层的类名。<br />**版本要求：** 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |
| onChange | EventHandle | 滚动选择 value 改变时触发，`event.detail = {value: value}` value 为数组，表示 picker-view 内的 picker-view-column index 索引 ，从 0 开始。 |
| onPickStart | EventHandle | 当滚动选择开始时候触发事件。 <br />**版本要求：** 基础库 [2.8.0](https://opendocs.alipay.com/mini/ide/framework-changelog-v2) 及以上。 |
| onPickEnd | EventHandle | 当滚动选择结束时候触发事件。<br />**版本要求：** 基础库 [2.8.0](https://opendocs.alipay.com/mini/ide/framework-changelog-v2) 及以上。 |
