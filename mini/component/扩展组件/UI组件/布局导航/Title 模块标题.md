# 简介

页面内每个容器模块中的标题模块。

## 扫码体验

![标题模块扫码体验](https://mdn.alipayobjects.com/afts/img/A*9qa2R532ADUAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=504Wr4J6f7VOZ42klFJH8wAAAABkMK8AAAAA)

# 使用

## Herbox

[小程序在线体验](https://herbox-embed.alipay.com/s/doc-aliui-title?theme=light&previewZoom=75&chInfo=openhome-doc)
## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "title",
  "usingComponents": {
    "title": "mini-ali-ui/es/title/index"
  }
}
```

### .axml 示例代码

```html
<title hasLine="true" type="more" onActionTap="titleMore">
  内部标题无 icon 展开气泡菜单
</title>
<title
  hasLine="true"
  iconURL="https://t.alipayobjects.com/images/T1HHFgXXVeXXXXXXXX.png"
  type="close"
  onActionTap="titleClose"
>
  内部标题可关闭
</title>
<title
  hasLine="true"
  className="changeColor"
  iconURL="https://gw.alipayobjects.com/mdn/miniProgram_mendian/afts/img/A*wiFYTo5I0m8AAAAAAAAAAABjAQAAAQ/original"
  type="arrow"
  onActionTap="titleGo"
>
  使用 class 修改样式
</title>
```

### .acss 示例代码

```css
.changeColor {
  font-size: 30px;
  color: #f32600;
}
```
```javascript
Page({
  data: {},
  onLoad() {},
  titleGo() {
    my.showToast({
      content: '点击箭头，可设置跳转',
    });
  },
  titleMore() {
    my.showToast({
      content: '点击更多，展开气泡菜单',
    });
  },
  titleClose() {
    my.showToast({
      content: '点击关闭，可设置关闭',
    });
  },
});
```

## 属性说明

| 属性   | 类型     | 描述   |
| ------ | -------- | ------ |
| className | String | 自定义 class。 |
| hasLine | Boolean | 是否有下划线。默认值：false |
| iconURL | String | 标题旁边的 icon URL。默认以背景图的方式展示在一个正方形的元素中。 |
| type | String | 标题可操作区域类型，默认为空（如 type 为空，`onActionTap` 无效）。按列表显示各类型：<br />- arrow：箭头<br />- close：关闭<br />- more：更多<br />- custom：自定义内容，需要传递名为 operation 的具名插槽；默认为空。<br />版本要求：custommini-ali-ui 1.1.3 及以上 |
| onActionTap | EventHandle | type 属性有具体值时可点击事件。默认值：`() => {}` |
