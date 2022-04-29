
# 简介
多项选择器组，内部由多个 [checkbox](/mini/component/checkbox) 组成。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/83de699255617343f90aff92ec0cba40.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/7b10f15e-ef39-42f9-a7c9-db0be94f41fa) 

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
| name | String | 组件名字，用于表单提交获取数据。 |
| onChange | EventHandle | 中选中项发生改变时触发， `detail = {value: 选中的 checkbox 项 value 的值}`。  |

