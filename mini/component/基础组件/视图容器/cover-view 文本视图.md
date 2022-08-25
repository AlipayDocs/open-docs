# 简介
覆盖在原生组件之上的文本视图。可覆盖的原生组件包括 [map](https://opendocs.alipay.com/mini/component/map)、[canvas](https://opendocs.alipay.com/mini/component/canvas)。

## 使用限制

- 版本要求基础库 1.10.0 及以上，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 实际效果请以真机为准。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/mdn/rms_d929c6/afts/img/A*JFj2RaJ7iKEAAAAAAAAAAABjARQnAQ#align=left&display=inline&height=1906&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/cover-view/index&defaultOpenedFiles=pages/cover-view/index&theme=light) 

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| onTap | EventHandle | 点击事件回调。<br />**版本要求：**基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |


# 常见问题

### 如何取消 cover-view 默认背景白色？
不支持更改背景色，建议更改字体颜色。

### cover-view 是否支持圆角和阴影？
小程序 acss 支持圆角和阴影，示例代码： 圆角：border-radius: 15%; 阴影：box-shadow: 10px 10px 5px #888888;
