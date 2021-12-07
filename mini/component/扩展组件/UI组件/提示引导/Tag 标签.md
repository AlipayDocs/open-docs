
# 简介
突出利益点、以及属性说明的标签。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*rZ49QIi3GLoAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=4uqeKb9sYskPuZ1kwVzoewAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-tag?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "Tag",
 "usingComponents": {
   "tag": "mini-ali-ui/es/tag/index",
   "list-item": "mini-ali-ui/es/list/list-item/index",
   "am-switch": "mini-ali-ui/es/am-switch/index"
 }
}
```

### .axml 示例代码
```html
<view style="padding: 12px;">
  <view style="display: flex; justify-content: space-evenly;">
    <tag size="lg" iconType="{{useIcon ? 'qr' : ''}}" ghost="{{ghost}}" type="primary">标签</tag>
    <tag size="lg" iconType="{{useIcon ? 'qr' : ''}}" ghost="{{ghost}}" type="warning">标签</tag>
    <tag size="lg" iconType="{{useIcon ? 'qr' : ''}}" ghost="{{ghost}}" type="danger">标签</tag>
    <tag size="lg" iconType="{{useIcon ? 'qr' : ''}}" ghost="{{ghost}}" type="success">标签</tag>
  </view>
  <view style="display: flex; justify-content: space-evenly; margin-top: 20px;">
    <tag size="sm" iconType="{{useIcon ? 'qr' : ''}}" ghost="{{ghost}}" type="primary">标签</tag>
    <tag size="sm" iconType="{{useIcon ? 'qr' : ''}}" ghost="{{ghost}}" type="warning">标签</tag>
    <tag size="sm" iconType="{{useIcon ? 'qr' : ''}}" ghost="{{ghost}}" type="danger">标签</tag>
    <tag size="sm" iconType="{{useIcon ? 'qr' : ''}}" ghost="{{ghost}}" type="success">标签</tag>
  </view>
  <view style="padding: 20px 10px;">
    <list-item>
      图标
      <am-switch slot="extra" onChange="setInfo" data-name="useIcon" checked="{{useIcon}}"/>
    </list-item>
    <list-item>
      线框样式
      <am-switch slot="extra" onChange="setInfo" data-name="ghost" checked="{{ghost}}"/>
    </list-item>
  </view>
</view>
```

### .js 示例代码
```javascript
Page({
  data: {},
  onLoad() {},
  setInfo(e) {
    const { dataset } = e.target;
    const { name } = dataset;
    this.setData({
      [name]: e.detail.value,
    });
  },
});
```



## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 类名称。 |
| type | String | 标签类型。<br />**可选值：** primary、success、warning、danger。<br />**默认值：** primary |
| iconType | String | 图标类型。 |
| size | String | 标签大小。<br />**可选值：** lg、sm。<br />**默认值：** lg |
| ghost | Boolean | 是否显示为线框的 tag 样式。<br />**可选值：** true、false。<br />**默认值：** false |


### slots
| **slotName** | **描述** |
| --- | --- |
| - | 标签内部文案。 |

