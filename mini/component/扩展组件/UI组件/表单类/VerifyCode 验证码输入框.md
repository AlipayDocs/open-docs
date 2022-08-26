# 简介

验证码输入框。

## 使用限制

受控模式，使用时需要用 onInput 事件来回设 value。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*0FtBQ5-KZ58AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=ptMqEchgrzRIQ4B5--IstQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-verify-code?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Verify-code",
  "usingComponents": {
    "verify-code": "mini-ali-ui/es/verify-code/index"
  }
}
```

### .axml 示例代码

```html
<view>
  <view style="margin-top: 10px;" />
  <view style="padding: 0 10px;">验证码框</view>
  <view style="margin-top: 10px;" />
  <verify-code
    onInput="onInput"
    value="{{verifyCode}}"
    onClear="onClear"
    last="{{true}}"
    countDown="{{10}}"
    initActive="{{false}}"
    onSend="onSend"
  ></verify-code>
</view>
```

### .js 示例代码

```javascript
Page({
  data: {
    verifyCode: '',
  },
  onSend() {
    my.alert({
      title: 'verify code sent',
    });
  },
  onInput(e) {
    this.setData({
      verifyCode: e.detail.value,
    });
  },
});
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义的 class。 |
| label | String | 自定义 label 文案。<br />**默认值：** 验证码 |
| labelCls | String | 自定义 label 的 class。 |
| inputCls | String | 自定义 input 的 class |
| last | Boolean | 是否为最后一行。<br />**默认值：** false |
| value | String | 输入框值。 |
| name | String | 组件名字，用于表单提交获取数据。 |
| placeholder | String | 占位符。 |
| placeholderStyle | String | 指定 placeholder 的样式。 |
| placeholderClass | String | 指定 placeholder 的样式类。 |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |
| maxlength | Number | 最大长度。<br />**默认值：** 140 |
| focus | Boolean | 获取焦点。<br />**默认值：** false |
| clear | Boolean | 是否带清除功能，仅 disabled 为 false 才生效。<br />**默认值：** true |
| onInput | (e: Object) => void | 键盘输入时触发 input 事件。 |
| onConfirm | (e: Object) => void | 点击键盘完成时触发。 |
| onFocus | (e: Object) => void | 聚焦时触发。 |
| onBlur | (e: Object) => void | 失去焦点时触发。 |
| onClear | () => void | 点击清除 icon 时触发。 |
| txtSend | String | 发送按钮的默认文案。<br />**默认值：** 发送验证码<br />**版本要求：** mini-ali-ui [1.1.2](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| txtSendAgain | String | 重发按钮的默认文案。<br />**默认值：** 重发验证码<br />**版本要求：** mini-ali-ui [1.1.2](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| txtCountDown | String | 按钮倒计时的默认文案（不包含倒计时）。<br />**默认值：** 秒后重试<br />**版本要求：** mini-ali-ui [1.1.2](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| initActive | Boolean | 是否主动触发发送按钮。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.1.3](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |

## Bug & Tip

当 `initActive` 为 true 时，组件在初次加载后就会自动进入倒计时状态；如需要在该状态下有提示信息展示，需自行处理。
