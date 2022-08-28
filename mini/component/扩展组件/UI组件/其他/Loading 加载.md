# 简介

loading 加载动画。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*8spKR7IFKE0AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=4jH-vtQojHPwBwOHtiLKtwAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-loading?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Loading",
  "usingComponents": {
    "loading": "mini-ali-ui/es/loading/index",
    "container": "mini-ali-ui/es/container/index"
  }
}
```

### .axml 示例代码

```html
加载中<loading size="80rpx" className="inlineBlock" />
<container hasTitle="{{true}}" title='loading size="6rpx"'>
  <loading size="6rpx" color="red" />
</container>
<container hasTitle="{{true}}" title='loading height="36rpx"'>
  <loading height="36rpx" color="red" />
</container>
<container hasTitle="{{true}}" title='loading height="36rpx" size="6rpx"'>
  <loading height="36rpx" size="6rpx" color="red" />
</container>
<container hasTitle="{{true}}" title='loading size="100px"'>
  <loading size="100px" color="red" />
</container>
<container hasTitle="{{true}}" title="loading">
  <loading color="blue" />
</container>
```

### .acss 示例代码

```css
.inlineBlock {
  display: inline-block;
  vertical-align: middle;
}
```

## 属性说明

| **属性**  | **类型** | **描述**                                       |
| --------- | -------- | ---------------------------------------------- |
| className | String   | 自定义 class。                                 |
| size      | String   | 设置 loading 尺寸大小。<br />**默认值**：100px |
| color     | String   | 设置 loading 的颜色。<br />**默认值**：#1677ff |

## Bug & Tip

- `size` 的值需要带单位。
- `color` 的值仅支持颜色关键词和十六进制的颜色值表示方式，如 red、#F00 等。
- mini-ali-ui 1.2.0 引入的 loading 组件 size 属性不正常问题，已经在 1.2.3 版本中修复，并且 1.2.3 版本对 1.2.0 版本的问题进行了适配兼容，但适配后部分机型仍有少许显示偏差，建议受影响的这部分应用开发者再进行人工检查和校正。
