
# 简介
列表项。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*iavDQpGB4n4AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=OxoTJzq0hvdzYy1DHa-xWQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-list-item?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "List",
  "usingComponents":{
    "list": "mini-ali-ui/es/list/index",
    "list-item": "mini-ali-ui/es/list/list-item/index"
  }
}
```

### .axml 示例代码
```html
<list>
 <view slot="header">
   列表头部
 </view>
 <list-item thumb="http://thumb.link.png"
   arrow="{{true}}"
   onClick="onItemClick"
   upperSubtitle="上副标题"
   lowerSubtitle="下副标题" >
   主标题
   <view slot="extra">
     辅助信息
   </view>
 </list-item>
 <view slot="footer">
   列表尾部
 </view></list>
```

### .js 示例代码
```javascript
Page({
 onItemClick() {
   my.alert({
     content: '列表项点击事件'
   })
 }})
```

### .acss 示例代码
```css
.setting {
  padding: 20px;
  overflow: scroll;
  box-shadow: inset 0px 1px 4px 0px rgba(204,204,204,1);
}
.gap {
  height: 10px;
}
.row {
  display: flex;
  align-items: center;
  padding: 0 30rpx;
  background-color: white;
}
.row-title {
  flex: 1;
  padding-top: 28rpx;
  padding-bottom: 28rpx;
  font-size: 34rpx;
  color: #000;
}
.row-extra {
  flex-basis: initial;
  font-size: 32rpx;
  color: #888;
  margin-right: 12px;
}
.row-arrow {
  width: 32rpx;
  height: 32rpx;
  margin-left: 16rpx;
}
.new-list-container {
  height: 100vh;
  display: flex;
  flex-direction: column;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| arrow | Boolean | 是否启用箭头。<br />**默认值：** true |
| thumb | String | 缩略图地址。 |
| index | String | 用于记录位置的 index，在事件回调中会将这个 index 回传。 |
| borderRadius | Boolean | 列表项是否圆角。<br />**默认值：** false |
| upperSubtitle | String | 上副标题。 | 
| lowerSubtitle | String | 下副标题。 |
| titlePosition | String | 主标题位置。<br />**可选值：** top、middle、bottom。<br />**默认值：** top |
| thumbSize | String | 缩略图大小。有缩略图时必填。<br />**默认值：** 40 px |
| onClick | Function | 点击列表项事件。 |
| last | Boolean | 用于处理下划线是否显示。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.1.0](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |


### slot
list-item 共有 6 个插槽，位置和名称如图表所示：

![|723x230](https://mdn.alipayobjects.com/afts/img/A*iw6UQKNO-MDRsghBvS3tZwBkAa8wAA/original?bz=openpt_doc&t=RhdIAmffc_U4P5nxwVp7fgAAAABkMK8AAAAA#align=left&display=inline&height=283&margin=%5Bobject%20Object%5D&originHeight=283&originWidth=888&status=done&style=none&width=888)

| **插槽名称** | **描述** |
| --- | --- |
| supporting | 列表头部插槽。 |
| default | 默认插槽，用于放置主标题。 |
| afterTitle | 主标题后面的插槽，可用于放置标签、图标。 |
| afterUpperSubtitle | 上副标题后面的插槽，可用于放置标签、图标。 |
| afterLowerSubtitle | 下副标题后面的插槽，可用于放置标签、图标。 |
| extra | 列表尾部插槽，用于放置辅助信息。 |


# FAQ
如要删除最后一个 list-item 的下划线，可以通过 list 长度判断，将最后一个 list-item 的 last 属性设为 true 即可。
