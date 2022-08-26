# 简介

结果页。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*RZ2wRbmVjwkAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=CoCuy7cSr1K1kcT35aQYNAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-message?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

.axml 示例代码

```html
<view>
  <message
    title="{{title}}"
    subTitle="{{subTitle}}"
    type="{{type}}"
    mainButton="{{mainButton}}"
    subButton="{{subButton}}"
    onTapMain="goBack"
  >
    <view slot="tips"
      >这里是通过
      <text style="color: red;">slot</text>
      插槽加入的内容，加入更多自定义内容。</view
    >
  </message>
  <radio-group class="radio-group" onChange="radioChange" name="lib">
    <label class="radio" a:for="{{items}}" key="label-{{index}}">
      <radio value="{{item.name}}" checked="{{item.checked}}" />
      <text class="radio-text">{{item.value}}</text>
    </label>
  </radio-group>
  <view>主标题</view>
  <input value="{{title}}" onInput="titleChange" />
  <view>副标题</view>
  <textarea value="{{subTitle}}" onInput="subtitleChange" />
  <checkbox onChange="onChange" />显示按钮
</view>
```

### .js 示例代码

```javascript
Page({
  data: {
    title: '操作成功',
    subTitle:
      '内容详情可折行，建议不超过两内容。也可以通过 slot="tips" 插入更具有功能性的提示。',
    type: 'success',
    items: [
      { name: 'success', value: 'success', checked: true },
      { name: 'fail', value: 'fail' },
      { name: 'info', value: 'info' },
      { name: 'warn', value: 'warn' },
      { name: 'waiting', value: 'waiting' },
    ],
  },
  onLoad() {},
  goBack() {
    my.navigateBack();
  },
  radioChange(e) {
    this.setData({
      type: e.detail.value,
    });
  },
  titleChange(e) {
    this.setData({
      title: e.detail.value,
    });
  },
  subtitleChange(e) {
    this.setData({
      subTitle: e.detail.value,
    });
  },
  onChange(e) {
    if (e.detail.value) {
      this.setData({
        mainButton: {
          buttonText: '主要操作',
        },
        subButton: {
          buttonText: '辅助操作',
        },
      });
    } else {
      this.setData({
        mainButton: null,
        subButton: null,
      });
    }
  },
});
```

## 属性说明

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | false | 自定义的 class。 |
| type | String | false | 状态类型。有 success、fail、info、warn、waiting 五种状态类型。<br />**默认值：** success |
| title | String | true | 主标题。 |
| subTitle | String | false | 副标题。 |
| mainButton | Object<buttonText, disabled> | false | 主按钮的文本和可用性相关。 |
| subButton | Object<buttonText, disabled> | false | 副按钮的文本和可用性相关。 |
| onTapMain | () => {} | false | 主按钮的点击函数。 |
| onTapSub | () => {} | false | 副按钮的点击函数。 |

### slots

| **slotName** | **描述** |
| --- | --- |
| tips | 可根据需要插入内容，如拨打客服电话等。当 subTitle 为空时才有效。 |
