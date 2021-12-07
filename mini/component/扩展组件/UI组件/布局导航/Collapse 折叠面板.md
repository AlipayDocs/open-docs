
# 简介
可以折叠 / 展开的内容区域。

- 对复杂区域进行分组和隐藏，保持页面的整洁；
- **手风琴模式** 是一种特殊的折叠面板，只允许单个内容区域展开。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*zPrfTYBFXaQAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=6VlOp_JCeXb8UFqBpZsovAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-collapse?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
  "defaultTitle": "Collapse",
  "usingComponents": {
    "collapse": "mini-ali-ui/es/collapse/index",
    "collapse-item": "mini-ali-ui/es/collapse/collapse-item/index"
  }
}
```

### .axml 示例代码
```html
<view>
  <view class="demo-title">基础用法</view>
  <collapse
    className="demo-collapse"
    collapseKey="collapse1"
    activeKey="{{['item-11', 'item-13']}}"
    onChange="onChange"
  >
    <collapse-item header="标题1" itemKey="item-11" collapseKey="collapse1">
      <view class="item-content">
        <block a:for="{{randomLine}}">
          <view>自适应高度的内容区域 共 {{index + 1}} 行</view>
        </block>
      </view>
    </collapse-item>
    <collapse-item header="标题2" itemKey="item-12" collapseKey="collapse1">
      <view class="item-content content2">
        <view>内容区域</view>
      </view>
    </collapse-item>
    <collapse-item header="标题3" itemKey="item-13" collapseKey="collapse1">
      <view class="item-content content3">
        <view>内容区域</view>
      </view>
    </collapse-item>
  </collapse>
  <view class="demo-title">手风琴模式</view>
  <collapse
    className="demo-collapse"
    collapseKey="collapse2"
    activeKey="{{['item-21', 'item-23']}}"
    onChange="onChange"
    accordion="{{true}}"
  >
    <collapse-item header="标题1" itemKey="item-21" collapseKey="collapse2">
      <view class="item-content">
        <block a:for="{{randomLine}}">
          <view>自适应高度的内容区域 共 {{index + 1}} 行</view>
        </block>
      </view>
    </collapse-item>
    <collapse-item header="标题2" itemKey="item-22" collapseKey="collapse2">
      <view class="item-content content2">
        <view>内容区域</view>
      </view>
    </collapse-item>
    <collapse-item header="标题3" itemKey="item-23" collapseKey="collapse2">
      <view class="item-content content3">
        <view>内容区域</view>
      </view>
    </collapse-item>
  </collapse>  
</view>
```

### .acss 示例代码
```css
.item-content {
  padding: 14px 16px;
  font-size: 17px;
  color: #333;
  line-height: 24px;
}
.content1 {
  height: 200px;
}
```

## 属性说明
Collapse 折叠面板主要是有 `<collapse>` 和 `<collapse-item>` 两部分组成，所以，属性也有所不同。

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| activeKey | Array / String | 当前激活 tab 面板的 key。<br />**默认值：** 默认无，accordion 模式下默认第一个元素 |
| onChange | EventHandle | 切换面板的回调。<br />**默认值：** (activeKeys: Array): void |
| accordion | Boolean | 是否为手风琴模式。<br />**默认值：** false |
| collapseKey | String | 唯一标示 collapse 和对应的 collapse-item。 |


### collapse-item
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| titleClass | String | 自定义标题的 class。 |
| contentClass | String | 自定义内容区域的 class。 |
| isOpen | Boolean | 面板内容是否展开。<br />**默认值：** false |
| showArrow | Boolean | 是否显示箭头。<br />**默认值：** true |
| itemKey | String | 对应 activeKey，组件唯一标识。。 |
| header | String | 面板头内容。 |
| collapseKey | String | 唯一标识 collapse-item 所对应的 collapse。 |
| disabled | Boolean | 当前面板是否可点击使用。<br />**默认值：** true |
| am-collapse-item-title | Slot | 面板头内容。 |


## Bug & Tip 

- 当页面中存在多个 collapse 组件时，collapse 所对应的 collapse-item 的 `collapseKey` 属性为必选值并且必须相等。
- 当页面中只有一个 collapse 组件时，`collapseKey` 不需要提供。
- 如 `accordion` 为 true 时，`activeKey` 传值仅为字符串，如果传数组将导致取值错误，展示默认的第一个。 
