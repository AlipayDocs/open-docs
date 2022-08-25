# 简介

可用于需要遮罩蒙层的弹层元素。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*R7BBTYwB74oAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=sa6Mi3J_bvFm4MxiD-d6bwAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-mask?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Mask",
  "usingComponents": {
    "mask": "mini-ali-ui/es/mask/index"
  }
}
```

### .axml 示例代码

```html
<mask
  type="{{type}}"
  show="{{show}}"
  maskZindex="{{maskZindex}}"
  onMaskTap="maskClick"
></mask>
```

### .js 示例代码

```javascript
Page({
  data: {
    type: 'market',
    maskZindex: 10,
  },
  maskClick() {
    if (this.data.type === 'market') {
      this.setData({
        type: 'product',
      });
    } else {
      this.setData({
        type: 'market',
        show: false,
      });
    }
  },
});
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| type | String | 显示不同透明度的蒙层。<br />**可选值：**<br />product：产品弹窗类型蒙层，透明度 0.55。<br />market：市场营销弹窗类型蒙层，透明度 0.75。<br />**默认值：** product |
| maskZindex | Number | 自定义蒙层的 z-index 层级。 |
| show | Boolean | 是否显示蒙层。 |
| onMaskTap | EventHandle | 蒙层点击事件。<br />**默认值：** () => { } |
| fixMaskFull | Boolean | 用以解决遮罩层受到 transform 影响而显示不全的问题。<br />**默认值：** false<br />**版本要求：** mini-ali-ui ﻿[1.0.11](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
