# 简介

用于让用户在不同的视图中进行切换。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*WsyHSJGoGNMAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=a8iGRMQiins5W8ZubeTGcQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-vtabs?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Vtabs",
  "usingComponents": {
    "vtabs": "mini-ali-ui/es/vtabs/index",
    "vtab-content": "mini-ali-ui/es/vtabs/vtab-content/index"
  }
}
```

### .axml 示例代码

```html
<vtabs
  tabs="{{tabs}}"
  onTabClick="handleChange"
  onChange="onChange"
  activeTab="{{activeTab}}"
  sameFontSize="{{false}}"
  tabBarlineShow="{{false}}"
>
  <block a:for="{{tabs}}">
    <vtab-content anchor="{{item.anchor}}">
      <view
        style="height: {{item.anchor === 'b'?'50vh':'100vh'}};background-color: {{item.anchor === 'b'?'#ccc':''}};"
      >
        <text>content of {{item.title}}</text>
      </view>
    </vtab-content>
  </block>
</vtabs>
```

### .js 示例代码

```javascript
Page({
  data: {
    activeTab: 2,
    tabs: [
      { title: '选项二', anchor: 'a', number: '6' },
      { title: '选项', anchor: 'b', number: '66' },
      { title: '不超过五字', anchor: 'c', number: '99+' },
      { title: '选项四选项四选项四选项四', anchor: 'd' },
      { title: '选项五', anchor: 'e' },
      { title: '选项六', anchor: 'f' },
    ],
  },
  handleChange(index) {
    this.setData({
      activeTab: index,
    });
  },
  onChange(index) {
    this.setData({
      activeTab: index,
    });
  },
});
```

## 属性说明

vtabs 纵向选项卡包含了 `<vtabs>` 和 `<vtab-content>` 两部分。

### vtabs

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| className | String | false | 自定义 class。 |
| activeTab | Number | false | 当前激活 Tab 索引。<br />**默认值：** 0 |
| tabs | Array<title, anchor> | true | tab 数据。 |
| animated | Boolean | false | 是否开启动画。<br />**默认值：** false |
| swipeable | Boolean | false | 是否可滑动切换。<br />**默认值：** true |
| tabBarActiveTextColor | String | false | tabBar 激活状态文字颜色。<br />**默认值：** #1677FF |
| tabBarActiveBgColor | String | false | tabBar 激活状态背景色。<br />**默认值：** #ffffff |
| tabBarInactiveTextColor | String | false | tabBar 非激活状态文字颜色。<br />**默认值：** #333333 |
| tabBarInactiveBgColor | String | false | tabBar 非激活状态背景色。<br />**默认值：** #f5f5f5 |
| tabBarlineColor | String | false | tabBar 激活状态边线。<br />**默认值：** #1677FF |
| onTabClick | EventHandle | false | tab 被点击的回调。<br />**默认值：** (index: Number) => void |
| onChange | EventHandle | false | vtab-content 变化时触发。<br />**默认值：** (index: Number) => void |
| sameFontSize | Boolean | false | tab 选项卡的文字是否保持相同，如为 false，激活态的文字会大一点。<br />**默认值：** true<br />**版本要求：** mini-ali-ui [1.0.6](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| tabBarlineShow | Boolean | false | tab 选项卡激活态侧边竖线是否显示。<br />**默认值：** true<br />**版本要求：** mini-ali-ui [1.0.6](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| onTabFirstShow | EventHandle | false | tab 选项卡首次出现时的回调。<br />**默认值：** (index: Number, anchor: String) => {}<br />**版本要求：** mini-ali-ui [1.0.12](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |

### vtab-content

| **属性** | **类型** | **必填** | **描述**         |
| -------- | -------- | -------- | ---------------- |
| anchor   | String   | true     | 列表唯一锚点值。 |

## Bug & Tip

- tabs 数组中需要包含 vtab-content 中的 anchor。
- tabs 数组的数据格式：`[{ title: '', anchor: '', number: '99+',},]`。
