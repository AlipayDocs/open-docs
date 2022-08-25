
# 简介
按钮，用户只需单击一下即可执行操作并做出选择。常用于表单提交、界面跳转、模块引导点击。具体用法和小程序框架中 [button](https://opendocs.alipay.com/mini/component/button) 保持一致，在 button 基础上做了样式的封装。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*-MwMSrAXKSAAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=mDIEfzP2RF0jHtlUvWJKjAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-button?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```plain
{
 "defaultTitle": "Button",
 "usingComponents": {
   "button": "mini-ali-ui/es/button/index",
   "radio": "mini-ali-ui/es/am-radio/index",
   "checkbox": "mini-ali-ui/es/am-checkbox/index"
 }
}
```

### .axml 示例代码
```html
<view class="container">
 <button onTap="onTest" showLoading="{{showLoading}}" dataName="{{dataName}}" type="{{type}}" subtitle="{{subtitle}}" disabled="{{disabled}}" shape="{{shape}}" capsuleSize="{{capsuleSize}}" capsuleMinWidth="{{capsuleMinWidth}}">
   {{title}}
 </button>
 <view>主标题</view>
 <input value="{{title}}" onInput="titleChange"/>
 <view>副标题</view>
 <input value="{{subtitle}}" onInput="subtitleChange"/>
 <view>按钮类型</view>
 <radio-group class="radio-group" onChange="typeChange" name="type">
   <label class="radio" a:for="{{types}}" key="label-{{index}}">
     <radio value="{{item.name}}" checked="{{item.checked}}" />
     <text class="radio-text">{{item.value}}</text>
   </label>
 </radio-group>
 <view>形状</view>
 <radio-group class="radio-group" onChange="shapeChange" name="shape">
   <label class="radio" a:for="{{shapes}}" key="label-{{index}}">
     <radio value="{{item.name}}" checked="{{item.checked}}" />
     <text class="radio-text">{{item.value}}</text>
   </label>
 </radio-group>
 <view>胶囊按钮大小</view>
 <radio-group class="radio-group" onChange="sizeChange" name="size">
   <label class="radio" a:for="{{capsuleSizes}}" key="label-{{index}}">
     <radio value="{{item.name}}" checked="{{item.checked}}" />
     <text class="radio-text">{{item.value}}</text>
   </label>
 </radio-group>
 <view>是否禁用</view>
 <checkbox onChange='onDisableChange'/>
 <view>是否限制胶囊按钮最小宽度</view>
 <checkbox onChange='onMinWidthChange'/>
 <view>是否现实loading</view>
 <checkbox onChange='onLoadingChange'/>
</view>
```

### .acss 示例代码
```css
.container {
  padding: 20rpx;
}
.container button {
  margin-bottom: 24rpx;
}
```

### .js 示例代码
```javascript
Page({
  data: {
    title: '按钮操作 Normal',
    subtitle: '',
    disabled: false,
    dataName: '1',
    type: '',
    shape: 'default',
    capsuleSize: 'medium',
    capsuleMinWidth: false,
    showLoading: false,
    types: [
      { name: 'default', value: 'default', checked: true },
      { name: 'primary', value: 'primary' },
      { name: 'ghost', value: 'ghost' },
      { name: 'text', value: 'text' },
      { name: 'warn', value: 'warn' },
      { name: 'warn-ghost', value: 'warn-ghost' },
      { name: 'light', value: 'light' },
    ],
    shapes: [
      { name: 'default', value: 'default', checked: true },
      { name: 'capsule', value: 'capsule' },
    ],
    capsuleSizes: [
      { name: 'small', value: 'small' },
      { name: 'medium', value: 'medium', checked: true },
      { name: 'large', value: 'large' },
    ],
  },
  onLoad() {
  },
  typeChange(e) {
    this.setData({
      type: e.detail.value,
    });
  },
  shapeChange(e) {
    this.setData({
      shape: e.detail.value,
    });
  },
  sizeChange(e) {
    this.setData({
      capsuleSize: e.detail.value,
    });
  },
  titleChange(e) {
    this.setData({
      title: e.detail.value,
    });
  },
  subtitleChange(e) {
    this.setData({
      subtitle: e.detail.value,
    });
  },
  onDisableChange(e) {
    this.setData({
      disabled: e.detail.value,
    });
  },
  onMinWidthChange(e) {
    this.setData({
      capsuleMinWidth: e.detail.value,
    });
  },
  onTap() {
    // e.target.dataset.name
  },
  onLoadingChange(e) {
    this.setData({
      showLoading: e.detail.value,
    });
  },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| type | String | 按钮样式。<br />**可选值：** default、primary、ghost、warn、warn-ghost、text、light<br />**默认值：** default |
| subtitle | String | 子标题。 |
| shape | String | 按钮形状。<br />**可选值：** default、capsule<br />**默认值：** default |
| capsuleSize | String | 胶囊按钮大小。<br />**可选值：** large、medium、small<br />**默认值：** medium |
| capsuleMinWidth | Boolean | 是否启用胶囊按钮最小宽度。<br />**可选值：** true、false<br />**默认值：** false |
| disabled | Boolean | 是否禁用。<br />**可选值：** true、false<br />**默认值：** false |
| showLoading | Boolean | 按钮文字前是否带 loading 图标。<br />**可选值：** true、false<br />**默认值：** false |
| hover-class | String | 按钮按下去的样式类。button-hover 默认为 {background-color: rgba(0, 0, 0, 0.1); opacity: 0.7;}，hover-class="none" 时表示没有点击态效果。<br />**默认值：** button-hover |
| hover-start-time | Number | 按住后多少时间后出现点击状态，单位毫秒。<br />**默认值：** 20 |
| hover-stay-time | Number | 手指松开后点击状态保留时间，单位毫秒。<br />**默认值：** 70 |
| hover-stop-propagation | Boolean | 是否阻止当前元素的祖先元素出现点击态。<br />**可选值：** true、false<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.10.0](https://docs.alipay.com/mini/framework/compatibility) 及以上 |
| form-type | String | 有效值：submit, reset，用于 [form](https://opendocs.alipay.com/mini/component/form) 组件，点击分别会触发 submit/reset 事件。 |
| open-type | String | 开放能力。<br />**版本要求：** mini-ali-ui [1.1.0](https://docs.alipay.com/mini/framework/compatibility) 及以上 |
| scope | String | 当 open-type 为 getAuthorize 时有效。<br />**版本要求：** mini-ali-ui [1.11.0](https://docs.alipay.com/mini/framework/compatibility) 及以上 |
| onTap | EventHandle | 点击。 |
| public-id | String | 生活号 ID，必须是当前小程序同主体且已关联的生活号，open-type="lifestyle" 时有效。 |

