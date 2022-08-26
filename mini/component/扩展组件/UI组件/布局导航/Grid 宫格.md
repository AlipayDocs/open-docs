# 简介

按照不同的业务场景，可选择不同列数的宫格，包含 2、3、4、5 列四种列数的宫格。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*gPTMQ4wkXFQAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=3vb1C51SZCjMRA8VwlA9aQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-grid?theme=light&previewZoom=75&chInfo=openhome-doc)

### .json 示例代码

```json
{
  "defaultTitle": "Grid",
  "usingComponents": {
    "grid": "mini-ali-ui/es/grid/index",
    "pagination": "mini-ali-ui/es/pagination/index"
  }
}
```

### .axml 示例代码

```html
<grid
  onGridItemClick="onItemClick"
  columnNum="{{5}}"
  list="{{list55}}"
  infinite="{{true}}"
  gridName="newGridName"
  circular="{{true}}"
  infiniteHeight="240rpx"
/>
```

### .js 示例代码

```javascript
Page({
  data: {
    list55: [
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '6标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
      {
        icon: 'https://gw.alipayobjects.com/zos/rmsportal/VBqNBOiGYkCjqocXjdUj.png',
        text: '标题文字',
      },
    ],
  },
  onItemClick(ev) {
    my.alert({
      content: ev.detail.index,
    });
  },
});
```

## 属性说明

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| columnNum | Number | true | 设置宫格的列数。仅在 3 列宫格中才有效果。<br />**可选值：** 2、3、4、5。<br />**默认值：** 3 |
| circular | Boolean | false | item 图是否为圆形。仅在 4/5 列宫格中才有效果。<br />**默认值：** false |
| list | Array | true | 宫格数据。 |
| onGridItemClick | EventHandle | false | 点击宫格项回调。<br />**默认值：** (index: Number) => void |
| hasLine | Boolean | false | 3 列宫格时才有的间隔线。<br />**默认值：** true |
| infinite | Boolean | false | 5 列宫格时是否为无限滚动模式。<br />**默认值：** false |
| multiLine | Boolean | false | 5 列宫格时是否以多行形式展示。默认值为 true 时，且未设置 `infinite` 的话，宫格最终会以 5 列多行的形式展示数据。<br />**默认值：** false<br />**版本要求：** mini-ali-ui [1.1.0](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| infiniteHeight | String | false | 无限滚动模式时的宫格整体高度。<br />**默认值：** 90px |
| gridName | String | false | 无限滚动宫格的名称。 |

## Bug & Tip

- `infinite` 无限滚动模式的宫格仅在 5 列宫格，且列数超过 5 条之后才会有效果。
- 如在一个页面中有多个无限滚动的 5 列宫格，建议增加使用 `gridName` 属性，避免分页符表现错误。
- 当使用 5 列的无限滚动时，需要同时引入 [pagination](https://opendocs.alipay.com/mini/component-ext/pagination) 组件。
