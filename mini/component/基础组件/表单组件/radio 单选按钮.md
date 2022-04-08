# 简介
单选按钮。

## 使用限制
- 不支持修改 radio 选中后的宽高。
- 不支持 radio 按钮 与 [text](/mini/component/text) 标签嵌套，支持平行关系。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/4b07417d74a2578ab1d5da6b5965507a.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

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
```javascript
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
| value | String | 组件值，选中时 change 事件会携带的 value。 |
| checked | Boolean | 当前是否选中。<br />**默认值：** false |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |
| color | String | radio 的颜色，同 CSS 色值。<br />**版本要求：** 基础库 [1.10.0](/mini/framework/compatibility) 及以上 |

