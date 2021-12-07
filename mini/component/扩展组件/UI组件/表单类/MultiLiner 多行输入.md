
# 简介
多行输入框，可输入多行内容。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*OqeGSr9t7GQAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=rfUxcdEKBHcjZxSKOvVjQAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-multi-liner?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "Multi-liner",
  "usingComponents": {
    "multi-liner": "mini-ali-ui/es/multi-liner/index"
  }
}
```

### .axml 示例代码
```html
<view>
  <view style="margin-top: 10px;" />
  <view class="title">多行输入</view>
  <multi-liner
    placeholder="字数统计↘" 
    value="{{value}}" 
    onInput="onInput" 
    last="{{true}}" 
    auto-height="{{true}}" 
    controlled="{{controlled}}"/>
  <view style="margin: 10px;" />
</view>
```

### .js 示例代码
```javascript
Page({
  data: {
    value: '内容',
    controlled: true,
  },
  onInput(e) {
    this.setData({
      value: e.detail.value,
    });
  },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义的 class。 |
| inputCls | String | 自定义 input 的 class。 |
| last | Boolean | 是否最后一行。<br />**默认值：** false |
| value | String | 初始内容。 |
| name | String | 组件名字，用于表单提交获取数据。 |
| placeholder | String | 占位符。 |
| placeholderStyle | String | 指定 placeholder 的样式。 |
| placeholderClass | String | 指定 placeholder 的样式类。 |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |
| maxlength | Number | 最大长度。<br />**默认值：** 140 |
| focus | Boolean | 获取焦点。<br />**默认值：** false |
| auto-height | Boolean | 是否自动增高。<br />**默认值：** false |
| show-count | Boolean | 是否渲染字数统计功能（是否删除默认计数器/是否显示字数统计）。<br />**默认值：** true |
| controlled | Boolean | 是否为受控组件。为 true 时，value 内容会完全受 setData 控制。 |
| onInput | (e: Object) => void | 键盘输入时触发 input 事件。 |
| onConfirm | (e: Object) => void | 点击键盘完成时触发。 |
| onFocus | (e: Object) => void | 聚焦时触发。 |
| onBlur | (e: Object) => void | 失去焦点时触发。 |


### Bug & tips
multi-liner 组件的特性主要来源于 [textarea](https://opendocs.alipay.com/mini/component/textarea)，当有光标或者文字输入相关疑惑，详情请参见 [textarea](https://opensupport.alipay.com/support/helpcenter/144/201602630402#anchor__3) [常见问题](https://opensupport.alipay.com/support/helpcenter/144/201602630402)。
