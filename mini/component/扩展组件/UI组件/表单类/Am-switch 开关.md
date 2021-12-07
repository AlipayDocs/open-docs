
# 简介
开关。具体用法和小程序框架中 switch 保持一致，在 switch 基础上做了样式的封装。

## 使用限制
iOS 和 Android 展现样式有所差异。iOS 单选开关为圆形；Android 单选开关为方形。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*RdlzRbedjA8AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=McT9o1a9mZlt8WWWPXCLIQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-am-switch?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "am-switch",
 "usingComponents": {
   "am-switch": "mini-ali-ui/es/am-switch/index"
 }
}
```

### .axml 示例代码
```html
<view class="page">
 <view class="page-description">开关</view>
 <view class="page-section">
   <view class="page-section-demo switch-list">
     <view class="switch-item">
       <am-switch checked onChange="switch1Change"/>
     </view>
     <view class="switch-item">
       <am-switch color="red" checked />
     </view>
   </view>
 </view>
</view>
```

### .js 示例代码
```javascript
Page({
 switch1Change(e) {
   console.log('switch1 发生 change 事件，携带值为', e.detail.value);
 },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| name | String | 组件名字，用于表单提交获取数据。 |
| checked | Boolean | 当前是否选中，可用来设置默认选中。<br />**可选值：** false、true<br />**默认值：** false |
| disabled | Boolean | 是否禁用。<br />**可选值：** false、true<br />**默认值：** false |
| onChange | (e: Object) => void | change 事件触发的回调函数。 |
| color | String | 组件颜色。<br />**可选值：** 同 CSS 色值 |
| controlled | Boolean | 是否为受控组件，为 true 时，checked 会完全受 setData 控制。<br />**可选值：** false、true<br />**默认值：** false |

