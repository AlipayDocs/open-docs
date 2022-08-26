# 简介

分页标识符。

## 扫码体验

![|154x191](https://mdn.alipayobjects.com/afts/img/A*vUeSRZiBv4EAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=WZGmMGHmAo6KgQF8JSYnnQAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-pagination?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Pagination",
  "usingComponents": {
    "pagination": "mini-ali-ui/es/pagination/index"
  }
}
```

### .js 示例代码

```html
<pagination pagerName='test1' infinite="true">
  <view style="display: flex;height: 100%;">
    <view style="text-align: center;padding-top: 20px;flex: 0 0 auto;width: 90vw;background-color: #f8d7d7;"><image src="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*whN9RZGSym8AAAAAAAAAAABkARQnAQ" style="width: 300rpx;height: 72rpx;" /></view>
    <view style="text-align: center;padding-top: 20px;flex: 0 0 auto;width: 90vw;background-color: #d5f7d5;"><image src="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*whN9RZGSym8AAAAAAAAAAABkARQnAQ" style="width: 300rpx;height: 72rpx;" /></view>
    <view style="text-align: center;padding-top: 20px;flex: 0 0 auto;width: 50vw;background-color: #f0e39e;"><image src="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*XMCgSYx3f50AAAAAAAAAAABkARQnAQ" style="width: 70px;height: 70px;"></view>
    <view style="text-align: center;padding-top: 20px;flex: 0 0 auto;width: 120vw;background-color: #F8F8F8;"><image src="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*whN9RZGSym8AAAAAAAAAAABkARQnAQ" style="width: 300rpx;height: 72rpx;" /></view>
    <view style="text-align: center;padding-top: 20px;flex: 0 0 auto;width: 20vw;background-color: #d3d3d3;"><image src="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*XMCgSYx3f50AAAAAAAAAAABkARQnAQ" style="width: 50px;height: 50px;"></view>
  </view>
</pagination>
<view style="width: 50vw;margin: 20px auto 0;background-color: #8f8f8f;">
  <pagination pagerName='test2' height="220rpx" white="true" infinite="true">
    <image src="https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*whN9RZGSym8AAAAAAAAAAABkARQnAQ" style="width: 779rpx;height: 186rpx;margin: 10px 20px;" />
  </pagination>
</view>
<view style="margin-top: 20px;">正常翻页样式</view>
<view style="padding: 20px 20px 0;background-color: #f8f8ba;">
  <pagination currentPage="{{3}}" max="{{10}}" height="200px" />
</view>
<view style="margin-top: 20px;">反白翻页样式</view>
<view style="padding: 20px 20px 0;background-color: #0e98d8;">
  <pagination currentPage="{{5}}" white="true" />
</view>
```

## 属性说明

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| className | String | 自定义 class。 |
| infinite | Boolean | 是否无限滚动分页。<br />**默认值：** false |
| fillColor | String | 无限滚动分页符背景色。<br />**默认值：** #ddd |
| frontColor | String | 无限滚动分页符颜色，当前页高亮颜色。<br />**默认值：** #006EFF |
| pagerName | String | 无限滚动分页符名称。 |
| height | String | 无限滚动分页容器的高度。<br />**默认值：** 100px |
| white | Boolean | 是否显示反白分页符。当 white 反白为 true 时，不可再修改颜色。<br />**默认值：** false |
| max | Number | 常规分页符最大显示数量。<br />**默认值：** 5 |
| currentPage | Number | 常规分页符当前页。<br />**默认值：** 1 |

## Bug&Tip

- 分页符组件共有两种模式：无限滚动模式和常规分页符：
  - 无限滚动模式 `<pagination infinite="{{true}}"></pagination>`。
  - 常规分页符：`<pagination />`。
- 无限滚动模式可通过 `fillColor` 和 `frontColor` 设置颜色。
- 常规分页符可通过 `frontColor` 改变当前页 icon 颜色。
- 无限滚动模式是双标签形式包含内容，可通过 height 设置容器高度。
- 如一个页面中存在多个无限滚动分页符，建议设置 pagerName，避免分页效果显示错误。
