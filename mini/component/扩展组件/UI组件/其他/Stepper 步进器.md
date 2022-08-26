# 简介

用作增加或者减少当前数值。

## 使用限制

- 输入最大值无提示，超过最大值时系统会自动回显数值为最大值。
- 不支持输入小数，可通过 + 和 - 改变数值大小。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*gqXoR7cfXEIAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=4OayCa-_FTmgpn0bxjykTQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-stepper?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Stepper",
  "usingComponents": {
    "stepper": "mini-ali-ui/es/stepper/index",
    "list": "mini-ali-ui/es/list/index",
    "list-item": "mini-ali-ui/es/list/list-item/index"
  }
}
```

### .axml 示例代码

```html
<list>
  <list-item disabled="{{true}}">
    Show number value
    <view slot="extra">
      <stepper
        onChange="callBackFn"
        step="{{1}}"
        showNumber
        readOnly="{{false}}"
        value="{{value}}"
        inputWidth="60px"
        min="{{2}}"
      />
    </view>
  </list-item>
  <list-item disabled="{{true}}">
    step: 0.01
    <view slot="extra">
      <stepper
        onChange="callBackFn"
        step="{{0.01}}"
        showNumber
        readOnly="{{false}}"
        value="{{value}}"
        min="{{2}}"
      />
    </view>
  </list-item>
  <list-item disabled="{{true}}">
    Do not show number value
    <view slot="extra">
      <stepper
        onChange="callBackFn"
        step="{{1}}"
        readOnly="{{false}}"
        value="{{value}}"
        min="{{2}}"
      />
    </view>
  </list-item>
  <list-item disabled="{{true}}">
    Disabled
    <view slot="extra">
      <stepper
        onChange="callBackFn"
        showNumber
        value="{{11}}"
        min="{{2}}"
        disabled
      />
    </view>
  </list-item>
  <list-item disabled="{{true}}">
    readOnly
    <view slot="extra">
      <stepper
        onChange="callBackFn"
        showNumber
        value="{{11}}"
        min="{{2}}"
        readOnly
      />
    </view>
  </list-item>
</list>
<button onTap="modifyValue">修改setper初始值</button>
```

### .js 示例代码

```javascript
Page({
  data: {
    value: 8,
  },
  callBackFn(value) {
    console.log(value);
  },
  modifyValue() {
    this.setData({
      value: 9,
    });
  },
});
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| min | Number | 最小值。<br />**默认值：** 0 |
| max | Number | 最大值。<br />**默认值：** 100000 |
| value | Number | 初始值。<br />**默认值：** 10 |
| step | Number | 每次改变步数，可以为小数。<br />**默认值：** 1 |
| onChange | EventHandle | 变化时回调函数。<br />**默认值：** (value: Number, mode: String) => void |
| disabled | Boolean | 是否禁用。<br />**默认值：** false |
| readOnly | Boolean | 是否只读。<br />**默认值：** false |
| showNumber | Boolean | 是否显示数值。<br />**默认值：** false |
| inputWidth | String | 输入框的宽度。<br />**默认值：** 36px |

## Bug & Tip

- `readOnly` 为 true 后，只可通过 + - 按钮来控制数字增加。
- `disabled` 为 true 后，步进器将不可用。
- 输入框的宽度由开发者自行设置，默认宽度为 36px。
- `onChange` 在 [1.0.11](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 版本中新增一个 mode 的返回值，用于判断用户是通过点击（click）还是通过输入（input）的方式改变值，两者之外就是 undefined。
