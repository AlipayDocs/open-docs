# 简介

位于列表右侧的次级信息组件，`list-secondary` 用于放在 `extra` 插槽，请参见 [`list-item`](https://opendocs.alipay.com/mini/component-ext/list-item) 组件。

## 扫码体验

![二维码](https://mdn.alipayobjects.com/afts/img/A*iavDQpGB4n55l25IgDrAHQBkAa8wAA/original?bz=openpt_doc&t=vX5JmSHEdEWubXP3L8eL-AAAAABkMK8AAAAA)
# 使用

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "List",
  "usingComponents": {
    "list": "mini-ali-ui/es/list/index",
    "list-item": "mini-ali-ui/es/list/list-item/index",
    "list-secondary": "mini-ali-ui/es/list/list-secondary/index"
  }
}
```

### .axml 示例代码

```html
<list>
  <view slot="header">列表头部</view>
  <list-item
    thumb="http://thumb.link.png"
    arrow="{{true}}"
    onClick="onItemClick"
    upperSubtitle="上副标题"
    lowerSubtitle="下副标题"
  >
  主标题
    <list-secondary
      title="次级标题"
      subtitle="次级副标题"
      thumb="http://thumb.url.jpg"
      thumbSize="20"
      slot="extra"
    />
  </list-item>
  <view slot="footer">列表尾部</view>
</list>
```
```javascript
Page({
  onItemClick() {
    my.alert({
      content: '列表项点击事件',
    });
  },
});
```

## 属性说明

| 属性   | 类型   | 描述                    |
| ------ | ------ | ----------------------- |
| thumb  | String | 缩略图地址。            |
| title  | String | 标题。                  |
| subtitle | String | 副标题。              |
| thumbSize | String | 缩略图大小。建议手动设值，不设值时图片的高度会有一定的自适应能力，但不能保证跟文案内容高度完全一致。有缩略图时必填。 |

### slot

`list-item` 组件共有 6 个插槽，位置和名称如下图所示。

![list-item 组件插槽示意图](https://mdn.alipayobjects.com/afts/img/A*iw6UQKNO-MDUx4BCh_j_VQBkAa8wAA/original?bz=openpt_doc&t=6gdZcQ4n912nP8uw3AK8uwAAAABkMK8AAAAA#align=left&display=inline&height=283&margin=%5Bobject%20Object%5D&originHeight=283&originWidth=888&status=done&style=none&width=888)
