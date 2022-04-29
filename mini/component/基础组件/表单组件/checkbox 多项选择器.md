# 简介
多选项目。

## 使用限制
checkbox 不支持修改选中的背景颜色样式。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/os/skylark-tools/public/files/7cff45f9018a7d0a966cfd0f097961b8.jpeg%26originHeight%3D157%26originWidth%3D127%26size%3D20801%26status%3Ddone%26width%3D127#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/1f7b18aa-c290-47f0-ae3a-84f11413c0b4)

### .axml 示例代码
```html
// API-DEMO page/component/checkbox/checkbox.axml 
<view class="page">
  <view class="page-description">多项选择器</view>
  <form onSubmit="onSubmit" onReset="onReset">
    <view class="page-section">
      <view class="page-section-title">选择你用过的框架：</view>
      <view class="page-section-demo">
        <checkbox-group onChange="onChange" name="libs">
          <label class="checkbox" a:for="{{items}}" key="label-{{index}}">
            <checkbox value="{{item.name}}" checked="{{item.checked}}" disabled="{{item.disabled}}" />
            <text class="checkbox-text">{{item.value}}</text>
          </label>
        </checkbox-group>
      </view>
      <view class="page-section-btns">
        <view><button type="ghost" size="mini" formType="reset">reset</button></view>
        <view><button type="primary" size="mini" formType="submit">submit</button></view>
      </view>
    </view>
  </form>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/checkbox/checkbox.js
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
    console.log('onSubmit', e);
    my.alert({
      content: `你选择的框架是 ${e.detail.value.libs.join(', ')}`,
    });
  },
  onReset(e) {
    console.log('onReset', e);
  },
  onChange(e) {
    console.log(e);
  },
});
```

### .acss 示例代码
```css
/* API-DEMO page/component/checkbox/checkbox.acss */
.checkbox {
  display: block;
  margin-bottom: 20rpx;
}
button + button {
  margin-top: 32rpx;
}
.checkbox-text {
  font-size:34rpx;
  line-height: 1.2;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| value | String | 组件值，选中时 change 事件会携带的 value。 |
| checked | Boolean | 当前是否选中，可用来设置默认选中。<br />**默认值：** false |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |
| onChange | EventHandle | 组件发生改变时触发，detail = {value: 该 checkbox 是否 checked }。 |
| color | String | checkbox 的颜色，同 CSS 色值。<br />**版本要求：** 基础库 [1.10.0](/mini/framework/compatibility) 及以上 |

