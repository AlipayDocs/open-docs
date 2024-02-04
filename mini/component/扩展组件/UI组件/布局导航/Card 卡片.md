# 简介

卡片。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*tPTnSI54PusAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=ngISZ3PEd03jNify0dMxKwAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

小程序在线体验，请访问：[Herbox](https://herbox-embed.alipay.com/s/doc-aliui-card?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### `.json` 示例代码

在小程序的 JSON 配置文件中，设置 `defaultTitle` 为 "Card"，并配置使用 `card` 组件，其路径为 "mini-ali-ui/es/card/index"。

```json
{
  "defaultTitle": "Card",
  "usingComponents": {
    "card": "mini-ali-ui/es/card/index"
  }
}
```
```html
<view class="container">
  <card title="卡片标题1" onCardClick="onCardClick" info="点击了第一个 card" />
  <view style="margin-top: 10px;" />
  <card 
    thumb="{{thumb}}" 
    title="卡片标题2" 
    subTitle="副标题非必填2" 
    onCardClick="onCardClick" 
    info="点击了第二个 card" 
  />
  <view style="margin-top: 10px;" />
  <view>
    <card 
      thumb="{{thumb}}" 
      title="卡片标题3" 
      subTitle="副标题非必填3" 
      onCardClick="toggle" 
      action="描述文字" 
      onActionClick="onActionClick" 
      extraAction="点击卡片展开/收起↑" 
      onExtraActionClick="onExtraActionClick" 
      info="点击了第三个 card" 
      expand="{{expand3rd}}" 
      bgImg="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*OjyRRqjLM6MAAAAAAAAAAABkARQnAQ" 
    />
  </view>
  <view style="margin-top: 10px;" />
  <view>
    <card 
      thumb="{{thumb}}" 
      title="卡片标题3" 
      subTitle="副标题非必填3" 
      onCardClick="onCardClick" 
      info="点击了第三个 card" 
      bgImg="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*OjyRRqjLM6MAAAAAAAAAAABkARQnAQ" 
      expand 
    /> 
  </view>
</view>
```
### .js 示例代码

```javascript
Page({
  data: {
    thumb: 'https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*b-kqQ4RZgsYAAAAAAAAAAABkARQnAQ',
    expand3rd: false
  },
  onCardClick(ev) {
    my.alert({
      content: ev.info
    });
  },
  onActionClick() {
    my.alert({
      content: 'action clicked'
    });
  },
  onExtraActionClick() {
    my.alert({
      content: 'extra action clicked'
    });
  },
  toggle() {
    this.setData({
      expand3rd: !this.data.expand3rd
    });
  }
});
```

## 属性说明

| 属性            | 类型     | 必填 | 描述                                                   |
| --------------- | -------- | ---- | ------------------------------------------------------ |
| thumb           | String   | 否   | Card 缩略图地址                                        |
| bgImg           | String   | 否   | Card 背景图地址                                        |
| title           | String   | 是   | Card 标题                                              |
| subTitle        | String   | 否   | Card 副标题                                            |
| action          | String   | 否   | 按钮文案，当有两个按钮时，action 在左侧                 |
| extraAction     | String   | 否   | 额外按钮文案，当有两个按钮时，extraAction 在右侧         |
| info            | String   | 否   | 用于点击卡片时往外传递数据                             |
| expand          | Boolean  | 否   | 卡片是否展开                                            |
| onActionClick   | Function | 否   | action 的点击事件回调                                  |
| onExtraActionClick | Function | 否   | extraAction 的点击事件回调                            |
| onCardClick     | Function | 否   | Card 点击的回调                                         |

- **默认值**：展开属性 `expand` 的默认值为 `false`。
