
# 简介
滑动选择器。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/5615dd2ce42f01988e82b704217c14d8.png#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-slider?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .axml 示例代码
```html
// API-DEMO page/component/slider/slider.axml 
<view class="page">
  <view class="page-description">滑块</view>
  <view class="page-section">
    <view class="page-section-title">设置step</view>
    <view class="page-section-demo">
      <slider value="5" onChange="slider2change" step="5"/>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">设置最小/最大值范围</view>
    <view class="page-section-demo">
      <slider value="33" onChange="slider4change" min="25" max="50" show-value/>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">自定义样式</view>
    <view class="page-section-demo">
      <slider value="33" onChange="slider4change" min="25" max="50" show-value
      backgroundColor="#FFAA00" activeColor="#00aaee" trackSize="2" handleSize="6" handleColor="blue" />
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/slider/slider.js
const pageData = {};
for (let i = 1; i < 5; ++i) {
  (function (index) {
    pageData['slider' + index + 'change'] = function (e) {
      console.log('slider' + index + '发生 change 事件，携带值为', e.detail.value);
    };
  })(i);
}
Page(pageData);
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| name | String | 组件名字，用于表单提交获取数据。 |
| min | Number | 最小值。<br />**默认值：** 0 |
| max | Number | 最大值。<br />**默认值：** 100 |
| step | Number | 步长，值必须大于 0，并可被(max - min)整除。<br />**默认值：** 1 |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |
| value | Number | 当前取值。<br />**默认值：** 0 |
| show-value | Boolean | 是否显示当前 value。<br />**默认值：** false |
| active-color | String | 已选择的颜色，同 CSS 色值。<br />**默认值：** #108ee9 |
| background-color | String | 背景条颜色，同 CSS 色值。<br />**默认值：** #ddd |
| track-size | Number | 轨道线条高度。<br />**默认值：** 4 |
| handle-size | Number | 滑块大小。<br />**默认值：** 22 |
| handle-color | String | 滑块填充色，同 CSS 色值。<br />**默认值：** #fff |
| onChange | EventHandle | 完成一次拖动后触发，`event.detail = {value: value}`。 |
| onChanging | EventHandle | 拖动过程中触发的事件，`event.detail = {value: value}`。<br />**版本要求：** 基础库版本 [1.5.0](/mini/framework/compatibility) 及以上 |

