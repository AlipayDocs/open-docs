# 简介

搜索提供了用户进行文本查询的功能，用户可以针对当前页面的内容通过精确搜索和模糊搜索进行内容筛选和定位，提高查询效率。搜索栏激活后出现取消按钮。

## 使用限制

仅用于 UI 展示没有对应的业务逻辑功能。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*cFR6T6YDzqIAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=ygcRtsAdl4OZ4KWbaCFW8QAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-search-bar?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Search-bar",
  "usingComponents": {
    "search-bar": "mini-ali-ui/es/search-bar/index"
  }
}
```

### .axml 示例代码

```html
<view>
  <search-bar
    value="{{value}}"
    focus="{{true}}"
    disabled="{{false}}"
    maxLength="{{20}}"
    showVoice="{{showVoice}}"
    placeholder="搜索"
    onInput="handleInput"
    onClear="handleClear"
    onCancel="handleCancel"
    onSubmit="handleSubmit"
    showCancelButton="{{false}}"
  />
</view>
<view
  >是否展示Voice图标
  <checkbox onChange="onChange" />
</view>
```

### .js 示例代码

```javascript
Page({
  data: {
    value: '',
    showVoice: false,
  },
  handleInput(value) {
    this.setData({
      value,
    });
  },
  handleClear() {
    this.setData({
      value: '',
    });
  },
  handleCancel() {
    this.setData({
      value: '',
    });
  },
  onChange(e) {
    this.setData({
      showVoice: e.detail.value,
    });
  },
});
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| value | String | 搜索框的当前值。 |
| placeholder | String | placeholder。 |
| focus | Boolean | 自动获取光标。<br />**可选值：** true、false。<br />**默认值：** false |
| showVoice | Boolean | 是否展示 voice 图标。<br />**可选值：** true、false。<br />**默认值：** false |
| onInput | (value: String) => void | 键盘输入时触发。 |
| onClear | (val: String) => void | 点击 clear 图标触发。 |
| onFocus | () => void | 获取焦点时触发。 |
| onBlur | () => void | 失去焦点时触发。 |
| onCancel | () => void | 点击取消时触发。 |
| onVoiceClick | () => void | 点击 voice 图标时触发。 |
| onSubmit | (val: String) => void | 点击键盘的 enter 时触发。 |
| disabled | Boolean | 设置禁用。<br />**可选值：** true、false。<br />**默认值：** false |
| maxLength | Number | 最多允许输入的字符个数。 |
| showCancelButton | Boolean | 是否一直显示取消按钮。<br />**可选值：** true、false。<br />**默认值：** false |
| borderColor | String | 搜索输入框边框色。<br />**默认值：** #1677ff |
| enableNative | Boolean | 如为 false 可处理 fixed 定位后输入框内容闪动的问题。<br />**默认值**：false |
| controlled | Boolean | 组件是否受控。<br />**默认值**：true |

## Bug & Tip

- searchBar 输入框在个别情况下会出现闪动的情况，需要使用 `enableNative` 进行处理，具体可参考 [input 输入框的使用限制](https://opendocs.alipay.com/mini/component/input#%E4%BD%BF%E7%94%A8%E9%99%90%E5%88%B6) 以及 [FAQ](https://opendocs.alipay.com/mini/component/input#FAQ) 部分的说明。<br />
- searchBar 输入框在手写输入情况下，部分安卓手机会出现连续输入现象，只需要将 controlled 属性设置为 false 即可。<br />
