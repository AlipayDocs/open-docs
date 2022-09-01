# 简介

用于引导新用户或者页面内的新功能使用说明。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*k-ugTaw0qaQAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=bgQvrbZfDias9tqx7Di5TQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-guide?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Guide",
  "usingComponents": {
    "guide": "mini-ali-ui/es/guide/index"
  }
}
```

### .axml 示例代码

```html
<guide
  show="{{guideShow}}"
  hasJump="{{guideJump}}"
  guideList="{{list}}"
  btn_next="看下一张引导图"
  btn_jump="直接关闭，不看跳过"
  btn_over="看完了😀啊"
  onGuideOver="closeGuide"
  maskClick="{{true}}"
></guide>
<button size="default" type="primary" onTap="onShowJumpGuide">
  查看可跳过的引导图
</button>
<button size="default" type="primary" onTap="onShowGuide">
  查看普通的引导图
</button>
```

### .js 示例代码

```css
Page({
 data: {
   list: [
     {
       url: 'https://gw.alipayobjects.com/as/g/dnestFEGroup/dnestCompetFE/0.3.54/public/ii_bg1.49350b69.jpg',
       x: '150rpx',
       y: '100rpx',
       width: '200px',
       height: '300px',
     },
     {
       url: 'https://gw.alipayobjects.com/as/g/dnestFEGroup/dnestCompetFE/0.3.54/public/ii_bg1.49350b69.jpg',
       x: '250rpx',
       y: '50rpx',
       width: '200px',
       height: '100px',
     },
     {
       url: 'https://gw.alipayobjects.com/as/g/dnestFEGroup/dnestCompetFE/0.3.54/public/ii_bg1.49350b69.jpg',
       x: '350rpx',
       y: '200rpx',
       width: '100px',
       height: '300px',
     },
     {
       url: 'https://gw.alipayobjects.com/as/g/dnestFEGroup/dnestCompetFE/0.3.54/public/ii_bg1.49350b69.jpg',
       x: '400rpx',
       y: '200rpx',
       width: '200rpx',
       height: '300rpx',
     },
   ],
 },
 onLoad() {},
 closeGuide() {
   this.setData({
     guideShow: false,
   });
 },
});
```

## 属性说明

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| btn_next | String | false | 引导按钮组中的下一步按钮的文案。<br />**默认值：** 下一步 |
| btn_jump | String | false | 引导按钮组中可跳过按钮的文案。<br />**默认值：** 跳过 |
| btn_over | String | false | 引导按钮组中，当引导内容在最后一页时按钮的文案。<br />**默认值：** 知道了 |
| hasJump | Boolean | false | 是否显示跳过按钮。<br />**默认值：** false |
| show | Boolean | false | 是否显示 guide 遮罩引导模块。<br />**默认值：** false |
| guideList | Array | true | guide 模块中的内容。<br />**默认值：** [] |
| onGuideOver | EventHandle | false | 跳过/关闭 guide 遮罩引导按钮的事件。<br />**默认值：** () => { } |
| maskClick | Boolean | false | 是否可通过点击遮罩触发事件。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.0.11](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |

## Bug & Tip

- `hasJump` 如为 false，guide 引导中的按钮只会显示一个 btn_next 按钮。
- `onGuideOver` 事件主要是用于控制当 guide 引导结束后或者当有跳过按钮出现时，点击按钮关闭 guide 引导的，如有必要也可以自行再添加事件。
- `guideList` 是用于控制显示每页 guide 引导图片的内容、位置以及大小等。
- 数组中的格式：`[{ url: '', x: '', y: '', width: '', height: '',},]`。
  - url：guide 引导图的 url。
  - x：引导图在可视区域的 x 坐标位置。
  - y：引导图在可视区域的 y 坐标位置。
  - width：引导图的宽度。
  - height：引导图的高度。
