# 简介
选择器包括一个或多个不同值的可滚动列表，每个值可以在视图的中心以较暗的文本形式显示。当用户正在编辑字段或点击菜单时，选择器通常会从屏幕底部弹起（iOS）或中间弹出（Android）。

## 使用说明
- picker 组件在 iOS 系统中从底部弹出，在 Android 系统中从中间弹出。
- 支持通过 [my.multiLevelSelect ](https://opendocs.alipay.com/mini/api/multi-level-select)调用级联选择。
- 支持通过 [my.datePicker](https://opendocs.alipay.com/mini/api/ui-date) 打开日期选择列表。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/6af93644fb19ed9be1d511fe208d4b20.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## 示例

[小程序在线](https://opendocs.alipay.com/examples/0fd1591a-cd48-4cb3-85dc-18e68ca30223) 

### .axml 示例代码
```html
<!-- API-DEMO page/component/picker/picker.axml -->
<view class="page">
  <view class="page-description">选择器</view>
  <view class="page-section">
    <picker onChange="bindPickerChange" value="{{index}}" range="{{array}}">
      <view class="row">
        <view class="row-title">地区选择器</view>
        <view class="row-extra">当前选择：{{array[index]}}</view>
        <image class="row-arrow" src="/image/arrowright.png" mode="aspectFill" />
      </view>
    </picker>
  </view>
  <view class="page-section">
    <picker onChange="bindObjPickerChange" value="{{arrIndex}}" range="{{objectArray}}" range-key="name">
      <view class="row">
        <view class="row-title">ObjectArray</view>
        <view class="row-extra">当前选择：{{objectArray[arrIndex].name}}</view>
        <image class="row-arrow" src="/image/arrowright.png" mode="aspectFill" />
      </view>
    </picker>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/picker/picker.js
Page({
  data: {
    array: ['中国', '美国', '巴西', '日本'],
    objectArray: [
      {
        id: 0,
        name: '美国',
      },
      {
        id: 1,
        name: '中国',
      },
      {
        id: 2,
        name: '巴西',
      },
      {
        id: 3,
        name: '日本',
      },
    ],
    arrIndex: 0,
    index: 0
  },
  bindPickerChange(e) {
    console.log('picker发送选择改变，携带值为', e.detail.value);
    this.setData({
      index: e.detail.value,
    });
  },
  bindObjPickerChange(e) {
    console.log('picker发送选择改变，携带值为', e.detail.value);
    this.setData({
      arrIndex: e.detail.value,
    });
  },
});
```

### .acss 示例代码
```javascript
/* API-DEMO page/component/picker/picker.acss */
.date-radio {
  padding: 26rpx;
}
.date-radio label + label {
  margin-left: 20rpx;
}
.row {
  display: flex;
  align-items: center;
  padding: 0 30rpx;
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
}
.row-arrow {
  width: 32rpx;
  height: 32rpx;
  margin-left: 16rpx;
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| title | String | 标题。 |
| range | String[] / Object[] | String[] 时表示可选择的字符串列表；Object[] 时需指定 range-key 表示可选择的字段。<br />**默认值：** [] |
| range-key | String | 当 `range` 为 Object[] 时，通过 range-key 来指定 Object 中 key 的值作为选择器显示内容。 |
| value | Number | 表示选择了 `range` 中的第几个（下标从 0 开始）。 |
| onChange | EventHandle | value 改变时触发，`event.detail = {value: value}`。 |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |

