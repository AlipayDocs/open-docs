# 简介

文本输入。

## 使用限制

- 输入区内容不折行，如用户输入的字数超出显示区，输入框内的文字可左右滑动。
- 如无特殊情况，清空按钮在框内有内容且获得焦点时默认出现。
- 在支付宝小程序容器中，原生 input 聚焦时如果同时抬升视图，可能出现光标抖动。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*dxShQq_ajv0AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=2gtI9okdyKpu-Ah9sjky6wAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-input-item?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "input-item",
  "usingComponents": {
    "list": "mini-ali-ui/es/list/index",
    "input-item": "mini-ali-ui/es/input-item/index",
    "am-icon": "mini-ali-ui/es/am-icon/index"
  }
}
```

### .axml 示例代码

```html
<view>
  <view style="margin-top: 10px;"></view>
  <list>
    <input-item
      data-field="cardNo"
      clear="{{false}}"
      value="{{cardNo}}"
      className="dadada"
      placeholder="银行卡号"
      onInput="onItemInput"
      onBlur="onItemBlur"
      onConfirm="onItemConfirm"
      onClear="onClear"
    >
      卡号
      <view slot="extra" class="extra" onTap="onExtraTap"></view>
    </input-item>
    <input-item
      data-field="name"
      placeholder="姓名"
      type="text"
      value="{{name}}"
      clear="{{true}}"
      onInput="onItemInput"
      onClear="onClear"
      >姓名</input-item
    >
    <input-item data-field="password" placeholder="密码">密码</input-item>
    <input-item
      data-field="layerShow1"
      placeholder="layer 为 vertical 的排列"
      type="text"
      layer="vertical"
      value="{{layerShow1}}"
      clear="{{true}}"
      onInput="onItemInput"
      onClear="onClear"
    >
      竖向表单
      <view onTap="onExtraTap" slot="extra">
        <am-icon type="phone-book_" size="24" color="#1677ef"></am-icon>
      </view>
    </input-item>
    <input-item
      data-field="layerShow2"
      placeholder="layer 为 vertical 的排列"
      type="text"
      layer="vertical"
      value="{{layerShow2}}"
      clear="{{true}}"
      onInput="onItemInput"
      onClear="onClear"
    >
      竖向表单
    </input-item>
    <input-item
      data-field="layerShow3"
      placeholder="layer 为 vertical 的排列"
      type="text"
      layer="vertical"
      disabled="{{true}}"
      value="{{layerShow3}}"
      clear="{{true}}"
      onInput="onItemInput"
      onClear="onClear"
    >
      竖向表单
      <view onTap="onExtraTap" slot="extra">
        <am-icon type="phone-book_" size="24" color="#1677ef"></am-icon>
      </view>
    </input-item>
    <input-item data-field="remark" placeholder="备注"></input-item>
  </list>
</view>
```

### .js 示例代码

```javascript
Page({
  data: {
    cardNo: '1234****',
    name: '',
    layerShow1: '',
    layerShow2: '垂直输入框的布局',
    layerShow3: 'disabled 状态的 input',
  },
  onExtraTap() {
    my.alert({
      content: 'extra tapped',
    });
  },
  onItemInput(e) {
    this.setData({
      [e.target.dataset.field]: e.detail.value,
    });
  },
  onItemFocus() {},
  onItemBlur() {},
  onItemConfirm() {},
  onClear(e) {
    this.setData({
      [e.target.dataset.field]: '',
    });
  },
  onSend() {
    my.alert({
      title: 'verify code sent',
    });
  },
});
```

### .acss 示例代码

```css
.extra {
  background-image: url('https://gw.alipayobjects.com/zos/rmsportal/dOfSJfWQvYdvsZiJStvg.svg');
  background-size: contain;
  background-repeat: no-repeat;
  background-position: right center;
  opacity: 0.2;
  height: 22px;
  width: 22px;
}
```

## 属性

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义的 class。 |
| labelCls | String | 自定义 label 的 class。 |
| inputCls | String | 自定义 input 的 class。 |
| last | Boolean | 是否最后一行。<br />**可选值：** true、false<br />**默认值：** false |
| value | String | 初始内容。 |
| name | String | 组件名字，用于表单提交获取数据。 |
| type | String | input 的类型。<br />**注意：** type 的属性值影响的是真机中的键盘类型，在 IDE 模拟器中并不一定会有效果。<br />**可选值：**<br /><ul><li>text： 字符输入框。</li><li>number： 纯数字输入框（ 0-9 之间的数字）。</li><li>idcard：身份证输入框（ 0-9 之间的数字，以及字符 x）。</li><li>digit：数字输入框，（ 0-9 之间的数字，以及小数点 . 字符，可用于含有小数的数字）。</li></ul> **默认值：** text |
| password | Boolean | 是否是密码类型。<br />**可选值：** true、false<br />**默认值：** false |
| placeholder | String | 占位符。 |
| placeholderStyle | String | 指定 placeholder 的样式。 |
| placeholderClass | String | 指定 placeholder 的样式类。 |
| disabled | Boolean | 是否禁用。<br />**可选值：** true、false<br />**默认值：** false |
| maxlength | Number | 最大长度。<br />**默认值：** 140 |
| focus | Boolean | 获取焦点。<br />**可选值：** true、false<br />**默认值：** false |
| clear | Boolean | 是否带清除功能，仅 disabled 为 false 才生效。<br />**可选值：** true、false<br />**默认值：** true |
| onInput | (e: Object) => void | 键盘输入时触发 input 事件。 |
| onConfirm | (e: Object) => void | 点击键盘完成时触发。 |
| onFocus | (e: Object) => void | 聚焦时触发。 |
| onBlur | (e: Object) => void | 失去焦点时触发。 |
| onClear | () => void | 点击清除 icon 时触发。 |
| layer | String | 文本输入框是否为垂直排列，vertical 时为垂直排列，空值为横向排列。<br />**可选值：** vertical<br />**版本要求：** mini-ali-ui [1.0.4](https://opendocs.alipay.com/mini/component-ext/ui-overview) 及以上 |
| controlled | Boolean | 是否为受控组件。详情请参见  [input 组件](https://opendocs.alipay.com/mini/component/input)。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.0.9](https://opendocs.alipay.com/mini/component-ext/ui-overview) 及以上 |

### Bug & tips

input-item 组件的特性主要来源于 [input](https://opendocs.alipay.com/mini/component/input)，当有光标或者文字输入相关疑惑，详情请参见 [input 常见问题](https://opendocs.alipay.com/support/01rb8r)。

## slots

| slotname | 必填  | **描述**                         |
| -------- | ----- | -------------------------------- |
| extra    | false | 用于渲染 input-item 项右边说明。 |

# FAQ

### 为何 setData 数据为空时，断点 money 值已经置空，但是在输入框还是显示 0？

this.setData 设置 data 为空时，不会渲染页面，建议使用组件的 clear。
