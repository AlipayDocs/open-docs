# 简介
多行输入框，可输入多行内容。支持使用 [my.hideKeyboard](https://opendocs.alipay.com/mini/api/ui-hidekeyboard) 接口隐藏输入键盘。可以在 [input](https://opendocs.alipay.com/mini/component/input) 组件中加上 `enableNative="{{false}}"`，避免 textarea 弹出键盘后出现内容上移。在 textarea 代码中加上 `enableNative="{{false}}"` ，可解决 Android 系统下 textarea 获取焦点的时候文字消失问题。

## 使用限制
- 不支持通过 textarea 获取键盘高度。
- 不支持 iOS 系统支付宝客户端版本 10.1.80 及以上使用 `focus=true` 自动唤起。
- 添加属性 `controlled="{{true}}" `表示 value 内容会完全受 setData 控制。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark/3e5f83dd-fcbe-43d6-9466-7259f98723c6/2018/jpeg/eab73793-ef6e-4a7c-b347-0044244a6ae1.jpeg#align=left&display=inline&height=1906&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-textarea?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .axml 示例代码
```html
<!-- API-DEMO page/component/textarea/textarea.axml -->
<view class="page">
  <view class="page-description">文本框</view>
  <view class="page-section">
    <view class="page-section-title">受控聚焦</view>
    <view class="page-section-demo">
      <textarea focus="{{focus}}" onFocus="onFocus" onBlur="onBlur" placeholder="Please input something" />
    </view>
    <view class="page-section-btns">
      <button type="default" size="mini" onTap="bindButtonTap">聚焦</button>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">自适应高度</view>
    <view class="page-section-demo">
      <textarea onBlur="bindTextAreaBlur" auto-height placeholder="Please input something" />
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">结合表单</view>
    <form onSubmit="bindFormSubmit">
      <view class="page-section-demo">
        <textarea name="textarea" placeholder="Please input something"  />
      </view>
      <view class="page-section-btns">
        <button form-type="submit" size="mini" type="primary">提交</button>
      </view>  
    </form>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/textarea/textarea.js
Page({
  data: {
    height: 20,
    focus: false,
  },
  bindButtonTap() {
    this.onFocus();
  },
  onFocus() {
    this.setData({
      focus: true,
    });
  },
  onBlur() {
    this.setData({
      focus: false,
    });
  },
  bindTextAreaBlur(e) {
    console.log(e.detail.value);
  },
  bindFormSubmit(e) {
    my.alert({
      content: e.detail.value.textarea,
    });
  },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| name | String | 组件名字，用于表单提交获取数据。 |
| value | String | 初始内容。 |
| placeholder | String | 占位符。 |
| placeholder-style | String | 指定 `placeholder` 的样式。<br />**版本要求：** 基础库 [1.6.0](/mini/framework/compatibility) 及以上 |
| placeholder-class | String | 指定 `placeholder` 的样式类。<br />**版本要求：** 基础库 [1.6.0](/mini/framework/compatibility) 及以上 |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |
| maxlength | Number | 最大长度，当设置为 -1 时不限制最大长度。<br />**默认值：** 140 |
| focus | Boolean | 获取焦点。<br />**默认值：** false |
| auto-height | Boolean | 是否自动增高。<br />**默认值：** false |
| show-count | Boolean | 是否渲染字数统计功能（**是否删除默认计数器/是否显示字数统计**）。<br />**默认值：** true<br />**版本要求：** 基础库 [1.8.0](/mini/framework/compatibility) 及以上 |
| controlled | Boolean | 是否为受控组件。为 true 时，value 内容会完全受 setData 控制。<br />**默认值：** false<br />**版本要求：** 基础库 [1.8.0](/mini/framework/compatibility) 及以上 |
| onInput | EventHandle | 键盘输入时触发，`event.detail = {value: value, cursor: cursor}`。<br />**版本要求**：`cursor` 字段基础库 [1.17.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上开始支持。 |
| onFocus | EventHandle | 输入框聚焦时触发 `event.detail = {value: value}`。 |
| onBlur | EventHandle | 输入框失去焦点时触发，`event.detail = {value: value}`。 |
| onConfirm | EventHandle | 点击完成时触发，`event.detail = {value: value}`。 |


