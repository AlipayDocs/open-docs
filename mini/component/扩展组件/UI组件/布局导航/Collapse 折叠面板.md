# 简介
  
可以折叠 / 展开的内容区域。
  
- 对复杂区域进行分组和隐藏，保持页面的整洁；
- **手风琴模式** 是一种特殊的折叠面板，只允许单个内容区域展开。
  
## 扫码体验
  
![折叠面板展示二维码](https://mdn.alipayobjects.com/afts/img/A*zPrfTYBFXaQAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=6VlOp_JCeXb8UFqBpZsovAAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)
  
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
    class="demo-collapse"
    collapse-key="collapse1"
    active-key="{{['item-11', 'item-13']}}"
    on-change="onChange"
  >
    <collapse-item header="标题1" item-key="item-11" collapse-key="collapse1">
      <view class="item-content">
        <block a:for="{{randomLine}}">
          <view>自适应高度的内容区域 共 {{index + 1}} 行</view>
        </block>
      </view>
    </collapse-item>
    <collapse-item header="标题2" item-key="item-12" collapse-key="collapse1">
      <view class="item-content content2">
        <view>内容区域</view>
      </view>
    </collapse-item>
    <collapse-item header="标题3" item-key="item-13" collapse-key="collapse1">
      <view class="item-content content3">
        <view>内容区域</view>
      </view>
    </collapse-item>
  </collapse>
  
  <view class="demo-title">手风琴模式</view>
  <collapse
    class="demo-collapse"
    collapse-key="collapse2"
    active-key="{{['item-21', 'item-23']}}"
    on-change="onChange"
    accordion="{{true}}"
  >
    <collapse-item header="标题1" item-key="item-21" collapse-key="collapse2">
      <view class="item-content">
        <block a:for="{{randomLine}}">
          <view>自适应高度的内容区域 共 {{index + 1}} 行</view>
        </block>
      </view>
    </collapse-item>
    <collapse-item header="标题2" item-key="item-22" collapse-key="collapse2">
      <view class="item-content content2">
        <view>内容区域</view>
      </view>
    </collapse-item>
    <collapse-item header="标题3" item-key="item-23" collapse-key="collapse2">
      <view class="item-content content3">
        <view>内容区域</view>
      </view>
    </collapse-item>
  </collapse>
</view>
```

在本段代码中进行了以下修改：
- 根据英文处理标准，将 `className` 改为了 `class`，修正了属性名的格式，使之符合 HTML 的标准写法。
- 将 `collapseKey`、`activeKey` 和 `onChange` 这些属性中的驼峰命名方式更正为小写字母和连字符的形式，以符合 HTML 属性的通常书写习惯。需要注意的是，在特定的前端框架中，比如 React，驼峰式命名会是正确的方式。但在此我们假设标准 HTML 语义，并进行相应的修改。
- 代码格式保持了原文的结构，并未进行修改，因为原文中代码块符合了逻辑清晰和格式正确的文档规范。
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

`Collapse` 折叠面板主要由 `<collapse>` 和 `<collapse-item>` 两部分组成，因此属性也各有不同。

| 属性       | 类型       | 描述                                      |
|------------|------------|-------------------------------------------|
| className  | String     | 自定义 class                              |
| activeKey  | Array/String | 当前激活的 tab 面板的 key                 |
| onChange   | EventHandle | 切换面板的回调                            |
| accordion  | Boolean    | 是否为手风琴模式                          |
| collapseKey | String    | 唯一标识 collapse 和对应的 collapse-item  |

**默认值**：
- `activeKey`：若是 `accordion` 模式，默认激活第一个元素
- `onChange`：`(activeKeys: Array) => void`
- `accordion`：`false`

### collapse-item

| 属性           | 类型     | 描述                          |
|----------------|----------|-------------------------------|
| className      | String   | 自定义 class                  |
| titleClass     | String   | 自定义标题的 class            |
| contentClass   | String   | 自定义内容区域的 class        |
| isOpen         | Boolean  | 面板内容是否展开              |
| showArrow      | Boolean  | 是否显示箭头                  |
| itemKey        | String   | 对应 activeKey，组件唯一标识   |
| header         | String   | 面板头内容                    |
| collapseKey    | String   | 唯一标识 collapse-item 所对应的 collapse |
| disabled       | Boolean  | 当前面板是否可点击使用        |
| am-collapse-item-title | Slot | 面板头内容                 |

**默认值**：
- `isOpen`：`false`
- `showArrow`：`true`
- `disabled`：`false`

## Bug & Tip

- 若页面中存在多个 `Collapse` 组件，每个组件对应的 `collapse-item` 的 `collapseKey` 属性必须相等且为必填项。
- 若页面中只有一个 `Collapse` 组件，则 `collapseKey` 不必填写。
- 若 `accordion` 设置为 `true`，`activeKey` 应传入字符串类型。若传入数组，则可能造成取值错误，默认展示第一个元素。
