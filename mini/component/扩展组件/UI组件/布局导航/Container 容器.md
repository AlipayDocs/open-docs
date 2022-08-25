# 简介

容器依据最佳实践统一了子元素的间距、圆角。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*pwAATYMd1QrJDSpHuG3BmgBkAa8wAA/original?bz=openpt_doc&t=vlZyr3VNmNSzHO8POSLb0wAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-container?theme=light&previewZoom=75&chInfo=openhome-doc)

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
<view className="container">
  <container
    className="container-item"
    title="带有 title 标题，可自定义设置"
    thumb="https://img.alicdn.com/tfs/TB1Go8lh9R26e4jSZFEXXbwuXXa-84-84.png"
    onActionTap="titleClick"
  >
    <view slot="operation" style="color: red;">is slot</view>
    <view class="item"
      >container 组件自带的 title 属性值效果。icon
      无值或者为空时，可插入一个名为 operation 的 slot 元素。</view
    >
  </container>
  <container
    className="container-item"
    title="带有 title 标题，箭头"
    icon="arrow"
    thumb="https://img.alicdn.com/tfs/TB1Q19sTNv1gK0jSZFFXXb0sXXa-112-112.png"
    onActionTap="titleClick"
  >
    <view class="item">container 组件自带的 title 属性值效果</view>
  </container>
  <container
    className="container-item"
    title="带有 title 标题，关闭"
    icon="close"
    thumb="https://img.alicdn.com/tfs/TB1Go8lh9R26e4jSZFEXXbwuXXa-84-84.png"
    onActionTap="titleClick"
  >
    <view class="item">container 组件自带的 title 属性值效果</view>
  </container>
  <container
    className="container-item"
    title="带有 title 标题，更多"
    icon="more"
    thumb="https://img.alicdn.com/tfs/TB1Q19sTNv1gK0jSZFFXXb0sXXa-112-112.png"
    onActionTap="titleClick"
  >
    <view class="item">container 组件自带的 title 属性值效果</view>
  </container>
  <container
    className="container-item"
    title="带有 title 标题，无"
    thumb="https://img.alicdn.com/tfs/TB1Go8lh9R26e4jSZFEXXbwuXXa-84-84.png"
    onActionTap="titleClick"
  >
    <view class="item">container 组件自带的 title 属性值效果</view>
  </container>
</view>
<view className="container">
  <container className="container-item">
    <view class="item">a1</view>
  </container>
  <container className="container-item">
    <view class="item">b1</view>
    <view class="item">b2</view>
  </container>
  <container className="container-item">
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
    <view slot="footer" class="footer" style="padding-left: 12px;"
      >底部展示区</view
    >
  </container>
  <container className="container-item">
    <title slot="header">滑动</title>
    <swiper indicator-dots="{{true}}" class="item">
      <block a:for="{{['#0abc80','#00b7f4']}}">
        <swiper-item>
          <view
            style="background-color: {{item}};width:100%;height:300rpx;border-radius:16rpx;"
          />
        </swiper-item>
      </block>
    </swiper>
  </container>
  <container className="container-item" type="onewithtwo">
    <view class="grid-item" style="height: 300rpx;" slot="first">first</view>
    <view class="grid-item" slot="second">second</view>
    <view class="grid-item" slot="third">third</view>
  </container>
</view>
```

### .js 示例代码

```javascript
Page({
  data: {},
  onLoad() {},
  titleClick() {
    my.alert({
      title: 'onActionTap 回调',
      content: '标题后面操作区域点击',
    });
  },
});
```

### .acss 示例代码

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
  margin-top: 24rpx;
}
.item {
  background: #eeeeee;
  text-align: center;
  height: 200rpx;
  padding-top: 20rpx;
}
.grid-item {
  background: #eeeeee;
  text-align: center;
}
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| type | String | 容器排版类型。<br />**可选值：** line（一行）、onewithtwo（一行两列）。type 为 line 时会等分所有子元素。<br />**默认值：** line |
| className | String | 自定义样式名。 |
| title | String | 当不为空时可展示  [title](https://opendocs.alipay.com/mini/component-ext/title)  组件。<br />**版本要求**：mini-ali-ui [1.2.0](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| thumb | String | 标题区域的 icon URL。<br />**版本要求**：mini-ali-ui [1.2.0](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| icon | String | 标题区域右侧的 icon 图标。<br />**可选值**：arrow、close、more。<br />**版本要求**：mini-ali-ui [1.2.0](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
| onActionTap | EventHandle | 标题区域右侧可点击事件。<br />**默认值**：() => {} <br />**版本要求**：mini-ali-ui [1.2.0](https://www.npmjs.com/package/mini-ali-ui?activeTab=versions) 及以上 |
