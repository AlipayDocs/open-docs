
# 简介
卡片。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*tPTnSI54PusAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=ngISZ3PEd03jNify0dMxKwAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-card?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "Card",
 "usingComponents":{
   "card":"mini-ali-ui/es/card/index"
 }
}
```

### .axml 示例代码
```html
<view class="container">
 <card title="卡片标题1"
   onCardClick="onCardClick"
   info="点击了第一个card" />
 <view style="margin-top: 10px;" />
 <card thumb="{{thumb}}"
   title="卡片标题2"
   subTitle="副标题非必填2"
   onCardClick="onCardClick"
   info="点击了第二个card" />
 <view style="margin-top: 10px;" />
 <view>
   <card thumb="{{thumb}}"
     title="卡片标题3"
     subTitle="副标题非必填3"
     onCardClick="toggle"
     action="描述文字"
     onActionClick="onActionClick"
     extraAction="点击卡片展开/收起↑"
     onExtraActionClick="onExtraActionClick"
     info="点击了第三个card"
     expand="{{expand3rd}}"
     bgImg="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*OjyRRqjLM6MAAAAAAAAAAABkARQnAQ" />
 </view>
 <view style="margin-top: 10px;" />
 <view>
   <card thumb="{{thumb}}"
     title="卡片标题3"
     subTitle="副标题非必填3"
     onCardClick="onCardClick"
     info="点击了第三个card"
     bgImg="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*OjyRRqjLM6MAAAAAAAAAAABkARQnAQ"
     expand
     />
</view>
```

### .js 示例代码
```javascript
Page({
 data: {
   thumb: 'https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*b-kqQ4RZgsYAAAAAAAAAAABkARQnAQ',
   expand3rd: false,
 },
 onCardClick(ev) {
   my.alert({
     content: ev.info,
   });
 },
 onActionClick() {
   my.alert({
     content: 'action clicked',
   });
 },
 onExtraActionClick() {
   my.alert({
     content: 'extra action clicked',
   });
 },
 toggle() {
   this.setData({
     expand3rd: !this.data.expand3rd,
   });
 },
});
```

## 属性说明
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| thumb | String | false | Card 缩略图地址。 |
| bgImg | String | false | Card 背景图地址。 |
| title | String | true | Card 标题。 |
| subTitle | String | false | Card 副标题。 |
| action | String | false | 按钮文案，当有两个按钮时 action 在左侧。 |
| extraAction | String | false | 额外按钮文案，当有两个按钮时 extraAction 在右侧。 |
| info | String | false | 用于点击卡片时往外传递数据。 |
| expand | Boolean | false | 卡片是否展开。<br />**默认值：** false |
| onActionClick | Function | false | action 的点击事件回调。 |
| onExtraActionClick | Function | false | extraAction 的点击事件回调。 |
| onCardClick | Function | false | Card 点击的回调。 |

