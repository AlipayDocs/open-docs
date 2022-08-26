# 简介

用作标签卡筛选。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*vSyvTL5GeJAAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=W1waafhpQGo-GEu68p5nYwAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-filter?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Filter",
  "usingComponents": {
    "filter": "mini-ali-ui/es/filter/index",
    "filter-item": "mini-ali-ui/es/filter/filter-item/index"
  }
}
```

### .axml 示例代码

```html
<filter show="{{show}}" max="{{1}}" equalRows="{{3}}">
  <block a:for="{{items}}">
    <filter-item
      value="{{item.value}}"
      subtitle="{{item.subtitle}}"
      id="{{item.id}}"
      onChange="handleCallBack"
      selected="{{item.selected}}"
      key="filter-item-{{key}}"
    />
  </block>
</filter>
```

### .js 示例代码

```javascript
Page({
  data: {
    show: true,
    items: [
      { id: 1, value: '衣服啊', selected: true },
      { id: 1, value: '橱柜' },
      { id: 1, value: '衣服' },
      { id: 1, value: '橱柜' },
      { id: 1, value: '衣服' },
      { id: 1, value: '橱柜' },
      { id: 1, value: '衣服' },
      { id: 1, value: '橱柜' },
      { id: 1, value: '橱柜' },
    ],
  },
  handleCallBack(data) {
    my.alert({
      content: data,
    });
  },
  toggleFilter() {
    this.setData({
      show: !this.data.show,
    });
  },
});
```

## 属性说明

### filter

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| show | Boolean | 是否显示。<br />**可选值：** true、false。<br />**默认值：** true |
| max | Number | 可选数量最大值，1 为单选。<br />**默认值：** 10000 |
| equalRows | Number | 把 filter-item 等分成 2 或者 3 列。<br />**可选值：** 2、3。 |
| onChange | (e: Object) => void | 多选时提交选中回调。 |
| onMaskTap | () => void | 点击遮罩层时触发，可用于关闭 filter。 |

### filter-item

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | false | 自定义样式。 |
| value | String | true | 值。 |
| id | String | false | 自定义标识符。 |
| selected | Boolean | false | 默认选中。<br />**可选值：** true、false。<br />**默认值：** false |
| onChange | (e: Object) => void | false | 单选时提交选中回调。 |

# FAQ

### Filter 组件是否能过滤，如果 value 里面有一串文字，过滤中间部分？

不支持。目前没有相关操作。

### 弹窗圆角限定值、高度范围分别是多少呢？

- filter 中的 item 元素对于圆角是可以自定义，目前值为 4px，如有需要可通过小程序开发者工具查找到相对应的类名，通过 CSS 重新定义覆盖样式。
- filter 中的内容列表区域最大高度是 415px（max-height: 415px;），如有需要也可通过小程序开发工具查找到相对应的类名去修改。
