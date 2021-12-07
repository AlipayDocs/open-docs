
# 简介
异常组件，主要分为全局异常与局部异常。

全局异常组件：提供了可爱的蚂蚁形象作为异常场景的反馈提示，包括网络问题和服务器问题，同时提供了对应的处理按钮。

局部异常组件：用于页面某个区块出现异常时的反馈提示，同时提供了对应的处理按钮。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*zYygR7epO_cAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=Odl4kKM5ksKxXaxUKwpCmAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-page-result?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "Page-result",
 "usingComponents": {
   "page-result": "mini-ali-ui/es/page-result/index"
 }
}
```

### .axml 示例代码
```html
<page-result
 type="network"
 title="网络不给力"
 brief="世界上最遥远的距离莫过于此"
 footer="{{footer}}"
 onTapLeft="onTapLeft"
 onTapRight="onTapRight"
/>
```

### .js 示例代码
```javascript
Page({
 data: {
   footer: [{
     text: '修复',
   }, {
     text: '刷新',
   }],
 },
 onTapLeft(e) {
   console.log(e, 'onTapLeft');
 },
 onTapRight(e) {
   console.log(e, 'onTapRight');
 },
});
```

## 倒计时模式
10 秒后可点击按钮（与 native 规范一致）。

### .axml 示例代码
```html
<!-- 倒计时模式 -->
<page-result
 type="busy"
 footer="{{footer}}"
 isCountDown="{{true}}"
 onTapLeft="onTapLeft"
/>
```

### .js 示例代码
```javascript
Page({
 data: {
   footer: [{
     text: '刷新',
   }],
 },
 onTapLeft(e) {
   console.log(e, 'onTapLeft');
 },
});
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| type | String | 异常页面类型。<br />**可选值：**<br />网络异常 network<br />服务繁忙 busy<br />服务异常 error<br />空状态 empty<br />用户注销 logoff<br />付款失败 payment<br />红包领空 redpacket<br />**默认值：** network |
| local | Boolean | 是否是局部异常内容。<br />**默认值：** false |
| title | String | 错误提示标题（最多一行）。<br />**默认值：** 默认文案 |
| brief | String | 错误提示简要（最多两行）。<br />**默认值：** 默认文案 |
| footer | Array[{text}] | 错误处理按钮文案（一个或两个按钮）。 |
| onTapLeft | EventHandle | （左侧）按钮事件处理函数。<br />**默认值：** e => {} |
| onTapRight | EventHandle | （右侧）按钮事件处理函数。<br />**默认值：** e => {} |
| isCountDown | Boolean | 是否设置倒计时模式。<br />**默认值：** false |
| countDownText | String | 倒计时提示的文案。<br />**默认值：** 重新刷新 |


## Bug & Tip 

- 异常组件新增五个非必选属性 footer、onTapLeft、onTapRight、isCountDown、countDownText。
- 组件提供默认 slot 的处理按钮（最多两个按钮），开发者也可自定义 slot 覆盖默认内容。
- 如需使用组件规范的处理按钮，请在 `footer` 中定义按钮的文案，配合 `onTapLeft` 和 `onTapRight` 方法，分别对应 footer[0] 和 footer[1] 的按钮实例（若只有一个按钮，只需定义 onTapLeft 属性）。
- 如需将操作按钮设置倒计时模式（仅一个按钮），可配置 `isCountDown` 属性，约定 10 秒的倒计时按钮（与 native 规范一致），默认文案为 10 秒后重新刷新，可通过 `countDownText` 配置替代 重新刷新 文案。
- 设置了倒计时模式，需要配合 `footer` 和 `onTapLeft` 属性定义倒计时后的处理按钮。
