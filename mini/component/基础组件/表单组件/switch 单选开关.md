
# 简介
单选开关。

## 使用限制

- iOS 和 Android 展现样式有所差异。iOS 单选开关为圆形，Android 单选开关为方形。
- 不支持自定义 switch 样式，如大小等。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/f5ca37ac5dfd5ae057504beb9ae059e5.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-switch?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .axml 示例代码
```html
// API-DEMO page/component/switch/switch.axml 
<view class="page">
  <view class="page-description">开关</view>
  <view class="page-section">
    <view class="page-section-demo switch-list">
      <view class="switch-item">
        <switch checked onChange="switch1Change" aria-label="{{switch1 ? 'switch opened' : 'switch closed'}}" />
      </view>
      <view class="switch-item">
        <switch onChange="switch2Change"/>
      </view>
      <view class="switch-item">
        <switch color="red" checked />
      </view>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/switch/switch.js
Page({
  data: {
    switch1: true,
  },
  switch1Change(e) {
    console.log('switch1 发生 change 事件，携带值为', e.detail.value);
    this.setData({
      switch1: e.detail.value,
    });
  },
  switch2Change(e){
    console.log('switch2 发生 change 事件，携带值为', e.detail.value);
  },
});
```

### .acss 示例代码
```css
/* API-DEMO page/component/switch/switch.acss */
.switch-item + .switch-item {
  margin-top: 20rpx;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| name | String | 组件名字，用于表单提交获取数据。 |
| checked | Boolean | 是否选中。 |
| disabled | Boolean | 是否禁用。 |
| color | String | 组件颜色，同 CSS 色值。<br />**版本要求：** 基础库 [1.10.0](/mini/framework/compatibility) 及以上 |
| onChange | EventHandle | checked 改变时触发，`event.detail={ value:checked}`。 |
| controlled | Boolean | 是否为受控组件，为 true 时，`checked` 会完全受 setData 控制。<br />**默认值：** false<br />**版本要求：** 基础库 [1.8.0](/mini/framework/compatibility) 及以上 |

