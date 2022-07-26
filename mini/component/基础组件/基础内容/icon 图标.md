
# 简介
图标。

## 使用限制
- icon组件不支持onTap、catchTap等点击事件。
- 跳转页面后左上角显示返回上一页 icon，不支持隐藏。
- icon 中所应用的样式如果是插件中的样式，建议修改样式定义的 `class` 名等信息，否则 icon 中不写插件代码显示正常，添加插件代码 icon 显示不正常。

##  扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/7380714f62c709478a9a507f9ff8450d.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 在线示例

[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/basic-component?view=preview&defaultPage=pages/icon/index&defaultOpenedFiles=pages/icon/index&theme=light) 

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| type | String | icon 类型。有效值： info、warn、waiting、cancel、download、search、clear、success、success_no_circle、loading。<br />**版本要求：** loading 支持基础库 [1.7.2](/mini/framework/compatibility) 及以上 |
| size | Number | icon 大小，单位 px。<br />**默认值：** 23 |
| color | String | icon 颜色，同 CSS 色值。 |

