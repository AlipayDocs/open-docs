
# 简介
当应用中需要比较明显的对用户当前的操作行为进行警示或提醒时，可以使用对话框。用户需要针对对话框进行操作后方可结束。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*8DxQRIGbf_LHBYxAptVsZABkAa8wAA/original?bz=openpt_doc&t=ZsjyBBDmakGMaX2q_d5uQQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-modal?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "Modal",
 "usingComponents": {
   "modal": "mini-ali-ui/es/modal/index"
 }
}
```

### .axml 示例代码
```html
<view>
  <button onTap="openModal">打开modal</button>
  <modal
    show="{{modalOpened}}"
    onModalClick="onModalClick"
    onModalClose="onModalClose"
    topImage="https://gw.alipayobjects.com/zos/rmsportal/yFeFExbGpDxvDYnKHcrs.png"
  >
    <view slot="header">标题单行</view>
    说明当前状态、提示用户解决方案，最好不要超过两行。
    <view slot="footer">确定</view>
  </modal>
</view>
```

### .js 示例代码
```javascript
Page({
  data: {
    modalOpened: false,
  },
  openModal() {
    this.setData({
      modalOpened: true,
    });
  },
  onModalClick() {
    this.setData({
      modalOpened: false,
    });
  },
  onModalClose() {
    this.setData({
      modalOpened: false,
    });
  }
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| show | Boolean | 是否展示 modal。<br />**可选值：** true、false。<br />**默认值：** false |
| showClose | Boolean | 是否渲染 关闭。<br />**可选值：** true、false。<br />**默认值：** false |
| mask | Boolean | 是否展示蒙层。<br />**可选值：** true、false。<br />**默认值：** true |
| closeType | String | 关闭图标类型。<br />**可选值：** 0-灰色图标；1-白色图标。<br />**默认值：** 0 |
| onModalClick | EventHandle | 选择区间时的回调。<br />**默认值：** () => void |
| onModalClose | EventHandle | 点击 关闭 的回调, showClose 为 false 时无需设置。<br />**默认值：** () => void |
| topImage | String | 顶部图片。 |
| topImageSize | String | 顶部图片规则.<br />**可选值：** lg (带图弹框-大图)<br />md (带图弹框)<br />sm(带图弹框-小图)<br />**默认值：** md |
| buttons | Array< Object > | 底部自定义多按钮，详情见 buttons 配置。<br />**默认值：** md |
| onButtonClick | EventHandle | 点击 buttons 部分的回调。<br />**默认值：** (e: Object) => void |
| buttonsLayout | String | 设置 buttons 的对齐方式。<br />**可选值：** horizontal，vertical。<br />**默认值：** horizontal |
| advice | Boolean | 是否是运营类弹窗。<br />**可选值：** true、false。<br />**默认值：** false |
| zIndex | String/Number | 设置弹框层级。 |
| disableScroll | Boolean | modal 展示时是否禁止页面滚动（以真机效果为准）。<br />**可选值：** true、false。<br />**默认值：** true |
| onMaskClick | EventHandle | 点击遮罩层时的回调。<br />**默认值：** () => void<br />**版本要求：** mini-ali-ui [1.1.2](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |


### buttons
提供按钮组配置，每一项表示一个按钮。

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| text | String | 按钮的文本。 |
| extClass | String | 按钮自定义 Class，可用户定制按钮样式。 |


### slots
| **slotName** | **必填** | **描述** |
| --- | --- | --- |
| header | false | modal 头部。 |
| footer | false | modal 尾部。 |

