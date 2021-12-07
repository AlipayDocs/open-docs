
# 简介
金额输入框。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*9104QYYFeUcAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=KykAPsGBc8V1cSdvjWnEAgAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-amount-input?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "amount-input",
 "usingComponents": {
   "amount-input": "mini-ali-ui/es/amount-input/index"
 }
}
```

### .axml 示例代码
```html
<view>
  <amount-input
    type="digit"
    title="转入金额"
    extra="建议转入¥100以上金额"
    placeholder="输入转入金额"
    value="{{value}}"
    maxLength="5"
    focus="{{true}}"
    btnText="全部提现"
    onClear="onInputClear"
    onInput="onInput"
    onConfirm="onInputConfirm" />
</view>
```

### .js 示例代码
```javascript
Page({
 data: {
   value: 200,
 },
 onInputClear() {
   this.setData({
     value: '',
   });
 },
 onInputConfirm() {
   my.alert({
     content: 'confirmed',
   });
 },
 onInput(e) {
   const { value } = e.detail;
   this.setData({
     value,
   });
 },
 onButtonClick() {
   my.alert({
     content: 'button clicked',
   });
 },
 onInputFocus() {},
 onInputBlur() {},
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| type | String | input 的类型。<br />**可选值：** digit、number。<br />**默认值：** number |
| title | String | 左上角标题。 |
| extra | String | 左下角说明。 |
| value | String | 输入框当前值。 |
| btnText | String | 右下角按钮文案。 |
| placeholder | String | placeholder。 |
| focus | Boolean | 自动获取光标。<br />**可选值：** true、false。<br />**默认值：** false |
| onInput | (e: Object) => void | 键盘输入时触发。 |
| onFocus | (e: Object) => void | 获取焦点时触发。 |
| onBlur | (e: Object) => void | 失去焦点时触发。 |
| onConfirm | (e: Object) => void | 点击键盘完成时触发。 |
| onClear | () => void | 点击 clear 图标触发。 |
| onButtonClick | () => void | 点击右下角按钮时触发。 |
| maxLength | Number | 最多允许输入的字符个数。 |
| controlled | Boolean | 是否为受控组件。为 true时，value 内容会完全受 setData 控制。<br />**可选值：** true、false。<br />**默认值：** false |
| showClear | Boolean | 是否一直显示清除 icon。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.1.3](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| focusAfterClear | Boolean | 清除 icon 触发后，输入框是否获得焦点。<br />**默认值：** true<br />**版本要求：** mini-ali-ui [1.1.3](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |

