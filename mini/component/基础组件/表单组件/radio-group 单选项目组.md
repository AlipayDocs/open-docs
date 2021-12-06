
# 简介
单项选择器组，内部由多个 [radio](/mini/component/radio)  组成。

## 扫码体验
![](https://gw.alipayobjects.com/zos/skylark-tools/public/files/26640e6c0b6e9f35420d563cef47ec7a.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-radio?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .axml 示例代码
```html
// API-DEMO page/component/radio/radio.axml 
<view class="page">
  <view class="page-description">单选框</view>
  <view class="page-section">
    <view class="section section_gap">
      <form onSubmit="onSubmit" onReset="onReset">
        <view class="page-section-demo">
          <radio-group class="radio-group" onChange="radioChange" name="lib">
            <label class="radio" a:for="{{items}}" key="label-{{index}}">
              <radio value="{{item.name}}" checked="{{item.checked}}" disabled="{{item.disabled}}" />
              <text class="radio-text">{{item.value}}</text>
            </label>
          </radio-group>
        </view>
        <view class="page-section-btns">
          <view><button size="mini" type="ghost" formType="reset">reset</button></view>
          <view><button size="mini" type="primary" formType="submit">submit</button></view>
        </view>
      </form>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/radio/radio.js
Page({
  data: {
    items: [
      { name: 'angular', value: 'AngularJS' },
      { name: 'react', value: 'React', checked: true },
      { name: 'polymer', value: 'Polymer' },
      { name: 'vue', value: 'Vue.js' },
      { name: 'ember', value: 'Ember.js' },
      { name: 'backbone', value: 'Backbone.js', disabled: true },
    ],
  },
  onSubmit(e) {
    my.alert({
      content: e.detail.value.lib,
    });
    console.log('onSubmit', e.detail);
  },
  onReset(e) {
    console.log('onReset', e);
  },
  radioChange(e) {
    console.log('你选择的框架是：', e.detail.value);
  },
});
```

### .acss 示例代码
```css
/* API-DEMO page/component/radio/radio.acss */
.radio {
  display: block;
  margin-bottom: 20rpx;
}
.radio-text {
  line-height: 1.8;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| onChange | EventHandle | 选中项发生变化时触发，`event.detail = {value: 选中项 radio 的 value}`。 |
| name | String | 组件名字，用于表单提交获取数据。 |

