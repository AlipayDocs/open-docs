# 简介

按照不同的业务场景，可选择不同列数的宫格，包括 2、3、4、5 列四种列数的宫格。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*gPTMQ4wkXFQAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=3vb1C51SZCjMRA8VwlA9aQAAAABkMK8AAAAA#align=left&display=inline&height=191&originHeight=191&originWidth=154&status=done&style=none&width=154)

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
        text: '标题文字 6',
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
      content: ev.detail.index.toString(),
    });
  },
});
```

对于上述代码的修改部分如下：

1. 对于包含数字的列表项（原文中的 '6标题文字'），根据文档标准将数字和文本之间添加空格，因此修改为 '标题文字 6'。
2. 添加了 `.toString()` 方法来转换 `ev.detail.index` 的数值为字符串，因为 `alert` 方法的 `content` 属性需要的是一个文本字符串。这个修改是为了防止在不同环境下可能出现的数据类型问题，确保代码的健壮性。
## 属性说明

| 属性        | 类型      | 必填  | 描述                                                         |
| ----------- | --------- | ----- | ------------------------------------------------------------ |
| columnNum   | Number    | 是    | 设置宫格的列数。仅在 3 列宫格中才有效果。<br />可选值：2、3、4、5。<br />默认值：3 |
| circular    | Boolean   | 否    | item 图是否为圆形。仅在 4/5 列宫格中才有效果。<br />默认值：false |
| list        | Array     | 是    | 宫格数据。                                                   |
| onGridItemClick | EventHandle | 否    | 点击宫格项回调。<br />默认值：(index: Number) => void         |
| hasLine     | Boolean   | 否    | 3 列宫格时才有的间隔线。<br />默认值：true                    |
| infinite    | Boolean   | 否    | 5 列宫格时是否为无限滚动模式。<br />默认值：false             |
| multiLine   | Boolean   | 否    | 5 列宫格时是否以多行形式展示。当默认值为 true，且未设置 `infinite` 时，宫格最终会以 5 列多行的形式展示数据。<br />默认值：false<br />版本要求：mini-ali-ui 1.1.0 及以上 |
| infiniteHeight | String | 否    | 无限滚动模式时的宫格整体高度。<br />默认值：90px              |
| gridName    | String    | 否    | 无限滚动宫格的名称。                                         |

## Bug & Tip

- `infinite` 无限滚动模式的宫格，只在 5 列宫格且列数超过 5 条之后起效。
- 若在一个页面中出现多个 5 列宫格的无限滚动，推荐使用 `gridName` 属性，以避免分页错误。
- 使用 5 列的无限滚动宫格时，需要同时引入 [pagination](https://opendocs.alipay.com/mini/component-ext/pagination) 组件。
