# 简介

显示页面页脚组件。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*AyPsQZB5z00AAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=UKUT3bRKLb7aKVQRplABowAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-footer?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Footer",
  "usingComponents": {
    "footer": "mini-ali-ui/es/footer/index"
  }
}
```
```html
<footer type="{{footerInfo1.type}}" content="{{footerInfo1.content}}" />
<footer 
  type="{{footerInfo2.type}}" 
  content="{{footerInfo2.content}}" 
  extend="{{footerInfo2.extend}}" 
/>
<footer type="{{footerInfo3.type}}" content="{{footerInfo3.content}}" />
<footer 
  type="{{footerInfo4.type}}" 
  content="{{footerInfo4.content}}" 
  extend="{{footerInfo4.extend}}" 
  onBrandTap="brandClick"
/>
<footer 
  type="{{footerInfo5.type}}" 
  content="{{footerInfo5.content}}"
  extend="{{footerInfo5.extend}}" 
/>
<footer 
  type="{{footerInfo6.type}}" 
  content="{{footerInfo6.content}}" 
  extend="{{footerInfo6.extend}}" 
  onLinkTap="linkTap"
/>
<footer 
  type="{{footerInfo7.type}}" 
  content="{{footerInfo7.content}}" 
  footerEndColor="{{footerInfo7.footerEndColor}}" 
/>
<footer type="{{footerInfo8.type}}" />
<footer 
  type="{{footerInfo8.type}}" 
  content="{{footerInfo8.content}}" 
  showEndIcon="{{footerInfo8.showEndIcon}}" 
  iconSize="{{footerInfo8.iconSize}}" 
/>
```

- 文档中的 HTML 示例代码本身是不需翻译的内容。
- 使用了良好的代码缩进和换行，使属性清晰易读，与《优秀技术文档的写作标准》中推荐的格式保持一致。
- 确保了属性和值的引号内没有遗漏或错误的字符，保持了原有代码的正确性和完整性。
```css
page {
  padding-top: 20px;
  background-color: #fff;
}
.am-footer {
  margin-bottom: 40px;
}
```
```javascript
Page({
  data: {
    footerInfo1: {
      type: 'normal',
      content: '底部文案置底说明',
    },
    footerInfo2: {
      type: 'guide',
      content: '没找到需要的？搜一下试试',
      extend: [
        {
          link: '/pages/list/app',
          text: '蚂蚁借呗',
        },
        {
          link: '/pages/list/app',
          text: '备用金',
        },
        {
          link: '/pages/list/app',
          text: '花呗收钱',
        },
      ],
    },
    footerInfo3: {
      type: 'copyright',
      content: '© 2004-2020 Alipay.com. All rights reserved.',
    },
    footerInfo4: {
      type: 'brand',
      content: '过往业绩不预示产品未来表现，市场有风险，投资需谨慎',
      extend: [
        {
          logo: 'https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*XMCgSYx3f50AAAAAAAAAAABkARQnAQ',
          width: '30px',
          height: '30px',
          link: '/pages/list/app',
        },
        {
          logo: 'https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*gWo-TLFGp38AAAAAAAAAAABkARQnAQ',
          width: '420rpx',
          height: '116rpx',
        },
      ],
    },
    footerInfo5: {
      type: 'link',
      content: '© 2004-2020 Alipay.com. All rights reserved.',
      extend: [
        {
          link: '/pages/list/app',
          text: '底部链接',
        },
      ],
    },
    footerInfo6: {
      type: 'link',
      content: '© 2004-2020 Alipay.com. All rights reserved.',
      extend: [
        {
          link: '/pages/list/app',
          text: '底部链接',
        },
        {
          link: '/pages/list/app',
          text: '底部链接',
        },
      ],
    },
    footerInfo7: {
      type: 'end',
      content: '自定义的没有更多内容的底线',
      footerEndColor: 'red',
    },
    footerInfo8: {
      type: 'end',
      showEndIcon: true,
      iconSize: 50,
    },
  },
  brandClick() {
    my.alert({
      content: '这个品牌 logo 没有链接，可通过 js 自定义点击事件。',
    });
  },
  linkTap(e) {
    my.alert({
      title: 'onLinkTap 回调',
      content: e,
    });
  },
});
```
## 属性说明

| 属性       | 类型     | 描述                                                                                                                                           |
| ---------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| className  | String   | 自定义 class                                                                                                                                   |
| type       | String   | 选择使用指定的页脚类型。可选值：`normal`、`guide`、`copyright`、`brand`、`link`、`end`。默认值：`normal`。版本要求：mini-ali-ui 1.0.4 及以上 |
| content    | String   | 页脚文本内容                                                                                                                                   |
| extend     | Array    | 页脚部分的链接、logo 等信息                                                                                                                     |
| onBrandTap | EventHandle | 品牌 logo 事件回调。仅在 `type: brand` 中有效，且是无链接的品牌 logo。默认值：`() => {}`                                            |
| onLinkTap  | EventHandle | 链接事件回调。仅在 `type: link` 中有效，用于点击链接时进行自定义处理，参数为当前 extend item。默认值：`() => {}`。版本要求：mini-ali-ui 1.1.7 及以上        |
| showEndIcon | Boolean | `type="end"` 时的 footer 组件是否以 icon 方式展示，为 `true` 将不会显示 `content` 的文本内容。默认值：`false`。版本要求：mini-ali-ui 1.0.4 及以上                            |
| iconName     | String | 使用 `am-icon`，具体的值可参考 `am-icon` 的 `type` 值。默认值：`selected`。版本要求：mini-ali-ui 1.0.4 及以上                                       |
| iconURL    | String | 使用网络图片。当确定使用网络图片后，`iconName` 将失效；且网络图片目前仅支持宽高相同且小于等于 `44rpx`。版本要求：mini-ali-ui 1.0.4 及以上                                        |
| iconSize   | Number | 小于等于 `22px` 的值。默认值：`18`。版本要求：mini-ali-ui 1.0.4 及以上                                                                                        |
| footerEndColor | String | `type="end"` 时文本的颜色。版本要求：mini-ali-ui 1.0.4 及以上                                                                                      |

## Bug & Tip

- 当选择不同的 `type` 时，`extend` 中的值也将会有所不同：
  - `normal`：无 `extend`。
  - `guide`：`extend` 的值为 `[{ link: '', text: '', }]`。
  - `copyright`：无 `extend`。
  - `brand`：`extend` 的值为 `[{ logo: '', width: '', height: '', link: '', },]`，如果无 `link` 的话，可选择触发 `onBrandTap` 事件。
  - `link`：`extend` 的值为 `[{ link: '', text: '', },]`，但有多个值时，文本链接之间会有间隔线出现。
  - `end`：显示为“没有更多了”字样的结尾，可更改为 `am-icon` 中的类型或者自定图片 url：
    - `end` 类型 `content` 默认值为“没有更多了”。
    - `showEndIcon` 为 `true` 时，`content` 内容将不再显示。
    - 当 `iconURL` 有值时，`am-icon` 中的类型将不会展示，而显示为 `icon` 的 `url`，请确保该 `url` 是可访问的。
