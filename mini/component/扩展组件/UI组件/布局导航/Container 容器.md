# 简介

容器依据最佳实践统一了子元素的间距、圆角。

## 扫码体验

![二维码示例 |154x191](https://mdn.alipayobjects.com/afts/img/A*pwAATYMd1QrJDSpHuG3BmgBkAa8wAA/original?bz=openpt_doc&t=vlZyr3VNmNSzHO8POSLb0wAAAABkMK8AAAAA#align=left&display=inline&height=191&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

[小程序在线体验](https://herbox-embed.alipay.com/s/doc-aliui-container?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Container",
  "usingComponents": {
    "container": "mini-ali-ui/es/container/index",
    "title": "mini-ali-ui/es/title/index"
  }
}
```
### .axml 示例代码

```html
<view class="container">
  <container
    class="container-item"
    title="带有 title 标题，可自定义设置"
    thumb="https://img.alicdn.com/tfs/TB1Go8lh9R26e4jSZFEXXbwuXXa-84-84.png"
    onActionTap="titleClick"
  >
    <view slot="operation" style="color: red;">is slot</view>
    <view class="item">
      container 组件自带的 title 属性值效果。icon 无值或者为空时，可插入一个名为 operation 的 slot 元素。
    </view>
  </container>
  <container
    class="container-item"
    title="带有 title 标题，箭头"
    icon="arrow"
    thumb="https://img.alicdn.com/tfs/TB1Q19sTNv1gK0jSZFFXXb0sXXa-112-112.png"
    onActionTap="titleClick"
  >
    <view class="item">container 组件自带的 title 属性值效果</view>
  </container>
  <container
    class="container-item"
    title="带有 title 标题，关闭"
    icon="close"
    thumb="https://img.alicdn.com/tfs/TB1Go8lh9R26e4jSZFEXXbwuXXa-84-84.png"
    onActionTap="titleClick"
  >
    <view class="item">container 组件自带的 title 属性值效果</view>
  </container>
  <container
    class="container-item"
    title="带有 title 标题，更多"
    icon="more"
    thumb="https://img.alicdn.com/tfs/TB1Q19sTNv1gK0jSZFFXXb0sXXa-112-112.png"
    onActionTap="titleClick"
  >
    <view class="item">container 组件自带的 title 属性值效果</view>
  </container>
  <container
    class="container-item"
    title="带有 title 标题，无"
    thumb="https://img.alicdn.com/tfs/TB1Go8lh9R26e4jSZFEXXbwuXXa-84-84.png"
    onActionTap="titleClick"
  >
    <view class="item">container 组件自带的 title 属性值效果</view>
  </container>
</view>
<view class="container">
  <container class="container-item">
    <view class="item">a1</view>
  </container>
  <container class="container-item">
    <view class="item">b1</view>
    <view class="item">b2</view>
  </container>
  <container class="container-item">
    <title
      slot="header"
      hasLine="true"
      showIcon="true"
      iconURL="https://gw.alipayobjects.com/mdn/miniProgram_mendian/afts/img/A*wiFYTo5I0m8AAAAAAAAAAABjAQAAAQ/original"
    >
      内部标题无操作
    </title>
    <view class="item">c1</view>
    <view class="item">c2</view>
    <view class="item">c3</view>
    <view slot="footer" class="footer" style="padding-left: 12px;">
      底部展示区
    </view>
  </container>
  <container class="container-item">
    <title slot="header">滑动</title>
    <swiper indicator-dots="{{true}}" class="item">
      <block a:for="{{['#0abc80','#00b7f4']}}">
        <swiper-item>
          <view style="background-color: {{item}}; width: 100%; height: 300rpx; border-radius: 16rpx;"></view>
        </swiper-item>
      </block>
    </swiper>
  </container>
  <container class="container-item" type="onewithtwo">
    <view class="grid-item" style="height: 300rpx;" slot="first">first</view>
    <view class="grid-item" slot="second">second</view>
    <view class="grid-item" slot="third">third</view>
  </container>
</view>
```

在修改过程中，HTML 代码块的中文内容进行了格式调整，主要涉及到以下方面：
- 修改了 `className` 为 `class`，因为在 HTML 中有效的属性应该是 `class` 而不是 `className`。
- 删除了无意义的行尾闭合标签斜线（例如 `<view />` 改为 `<view>`），这些斜线在 HTML5 中是不需要的。
- 删除了多余的换行符和空格，使代码更整洁。
- 规范了注释的位置，以避免行内注释可能导致的代码解析错误。
- 确保所有标签的属性和值都使用了双引号进行了包裹，并确保所有双引号内没有多余的空格。
- 确保了整个代码块的缩进是统一的，方便阅读。

以上修改保证了代码块在遵循 HTML 规范的同时，仍然保持其原有的结构和意图，且更加便于阅读和理解。
```javascript
Page({
  data: {},
  onLoad() {}, // 页面加载时执行的初始化工作
  titleClick() { // 处理标题点击事件
    my.alert({
      title: 'onActionTap 回调',
      content: '标题后面操作区域点击',
    });
  }, // 注意：逗号用于分隔对象内的属性或方法
});
```

```css
.container {
  background: #f5f5f5;
  padding: 24rpx;
  height: 100%;
}
.container-item {
  margin-bottom: 24rpx;
}
.footer {
  color: #333;
  margin-top: 24rpx; /* 页脚颜色和上边距设置 */
}
.item {
  background: #eeeeee;
  text-align: center;
  height: 200rpx;
  padding-top: 20rpx; /* 项目样式设置，包括背景、文本对齐、高度和上内边距 */
}
.grid-item {
  background: #eeeeee;
  text-align: center; /* 网格项样式设置 */
}
```
## 属性说明

| 属性     | 类型     | 描述 |
|----------|----------|------|
| type     | String   | 容器排版类型。可选值：`line`（一行）、`onewithtwo`（一行两列）。`type` 为 `line` 时会等分所有子元素。默认值：`line` |
| className| String   | 自定义样式名。|
| title    | String   | 当不为空时可展示 [title](https://opendocs.alipay.com/mini/component-ext/title) 组件。版本要求：mini-ali-ui 1.2.0 及以上 |
| thumb    | String   | 标题区域的 icon URL。版本要求：mini-ali-ui 1.2.0 及以上 |
| icon     | String   | 标题区域右侧的 icon 图标。可选值：`arrow`、`close`、`more`。版本要求：mini-ali-ui 1.2.0 及以上 |
| onActionTap | EventHandle | 标题区域右侧可点击事件。默认值：`() => {}` 版本要求：mini-ali-ui 1.2.0 及以上 |
