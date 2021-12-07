
# 简介
长密码框。

## 使用限制
受控模式，使用时需要用 onInput 事件来回设 value。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*UCLtQJC8q68AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=CqzwHAcMCOuwiY2WbZee4AAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-long-password?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```
{
  "defaultTitle": "verify-code",
  "usingComponents":{
    "long-password": "mini-ali-ui/es/long-password/index"
  }
}
```

### .axml 示例代码
```
<view>
  <view style="margin-top: 10px;" />
  <view style="padding: 0 10px;">长密码框</view>
  <view style="margin-top: 10px;" />
  <long-password
    placeholder="" 
    value="{{longPassword}}" 
    clear="{{true}}" 
    onInput="onInput" 
    onClear="onClear" />
</view>
```

### .js 示例代码
```
Page({
  data: {
    longPassword: '',
  },
  onInput(e) {
    this.setData({
      longPassword: e.detail.value,
    });
  },
  onClear() {
    this.setData({
      longPassword: '',
    });
  },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义的 class。 |
| inputCls | String | 自定义 input 的 class。 |
| last | Boolean | 是否是最后一行。<br />**默认值：**  false |
| value | String | 初始内容。 |
| name | String | 组件名字，用于表单提交获取数据。 |
| placeholder | String | 占位符。 |
| placeholderStyle | String | 指定 placeholder 的样式。 |
| placeholderClass | String | 指定 placeholder 的样式类。 |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |
| maxlength | Number | 最大长度。<br />**默认值：** 140 |
| focus | Boolean | 获取焦点。<br />**默认值：** false |
| clear | Boolean     | 是否带清除功能，仅 disabled 为 false 才生效。<br />**默认值：** true |
| onInput | (e: Object) => void | 键盘输入时触发input事件。 |
| onConfirm | (e: Object) => void | 点击键盘完成时触发。 |
| onFocus | (e: Object) => void | 聚焦时触发。 |
| onBlur | (e: Object) => void | 失去焦点时触发。 |
| onClear | (e: Object) => void | 点击清除 iCON 时触发。 |

