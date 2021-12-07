
# 简介
弹出菜单。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*ATcjRKr8C5AAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=i6VQeJ7lemdBInJkDOPs5QAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-popup?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "Popup",
 "usingComponents": {
   "popup": "mini-ali-ui/es/popup/index"
 }
}
```

### .axml 示例代码
```html
<view>
 <view class="btn-container">
   <button onTap="onTopBtnTap">弹出popup</button>
 </view>
 <popup show="{{showTop}}" position="top" onClose="onPopupClose">
   <view style="height: 200px; background: #fff; display: flex; justify-content: center; align-items: center;">hello world</view>
 </popup>
</view>
```

### .js 示例代码
```javascript
Page({
 data: {
   showTop: false,
 },
 onTopBtnTap() {
   this.setData({
     showTop: true,
   });
 },
 onPopupClose() {
   this.setData({
     showTop: false,
   });
 },
});
```

## 属性说明
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | false | 自定义 class。 |
| show | Boolean | false | 是否显示菜单。<br />**默认值：** false |
| animation | Boolean | false | 是否开启动画。<br />**默认值：** true |
| mask | Boolean | true | 是否显示 mask，不显示时点击外部不会触发 onClose。<br />**默认值：** true |
| position | String | true | 控制从什么方向弹出菜单，bottom 表示底部，left 表示左侧，top 表示顶部，right 表示右侧。<br />**默认值：** bottom |
| disableScroll | Boolean | false | 展示 mask 时是否禁止页面滚动。<br />**默认值：** true |
| zIndex | Number | false | 定义 popup 的层级。 |


## slots
可以在 popup 组件中定义要展示部分，具体可参看示例代码。 
