
# 简介
CSS flex 布局的封装。

## 扫码体验
![|154x191](https://mdn.alipayobjects.com/afts/img/A*xDjERrdrKNgAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=HwadADoddxwKvylwyWSy5wAAAABkMK8AAAAA#align=left&display=inline&height=191&margin=%5Bobject%20Object%5D&originHeight=191&originWidth=154&status=done&style=none&width=154)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-flex?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
{
 "defaultTitle": "Flex",
 "usingComponents": {
   "flex": "mini-ali-ui/es/flex/index",
   "flex-item": "mini-ali-ui/es/flex/flex-item/index"
 }
}
```

### .axml 示例代码
```html
<view class="flex-container">
 <view class="sub-title">Basic</view>
 <flex>
   <flex-item><view class="placeholder">Block</view></flex-item>
   <flex-item><view class="placeholder">Block</view></flex-item>
 </flex>
 <view style="height: 20px;" />
 <flex>
   <flex-item><view class="placeholder">Block</view></flex-item>
   <flex-item><view class="placeholder">Block</view></flex-item>
   <flex-item><view class="placeholder">Block</view></flex-item>
 </flex>
 <view style="height: 20px;" />
 <flex>
   <flex-item><view class="placeholder">Block</view></flex-item>
   <flex-item><view class="placeholder">Block</view></flex-item>
   <flex-item><view class="placeholder">Block</view></flex-item>
   <flex-item><view class="placeholder">Block</view></flex-item>
 </flex>
 <view className="sub-title">Wrap</view>
 <flex wrap="wrap">
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
 </flex>
 <view className="sub-title">Align</view>
 <flex justify="center">
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
 </flex>
 <flex justify="end">
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
 </flex>
 <flex justify="between">
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline">Block</view>
 </flex>
 <flex align="start">
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline small">Block</view>
   <view class="placeholder inline">Block</view>
 </flex>
 <flex align="end">
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline small">Block</view>
   <view class="placeholder inline">Block</view>
 </flex>
 <flex align="baseline">
   <view class="placeholder inline">Block</view>
   <view class="placeholder inline small">Block</view>
   <view class="placeholder inline">Block</view>
 </flex>
</view>
```

### .acss 示例代码
```css
.flex-container {
 padding: 10px;
}
.sub-title {
 color: #888;
 font-size: 14px;
 padding: 30px 0 18px 0;
}
.placeholder {
 background-color: #ebebef;
 color: #bbb;
 text-align: center;
 height: 30px;
 line-height: 30px;
 width: 100%;
}
.placeholder.inline {
 width: 80px;
 margin: 9px 9px 9px 0;
}
.placeholder.small {
 height: 20px;
 line-height: 20px
}
```

### .js 示例代码
```javascript
Page({});
```

## 属性说明
Flex 布局是由 flex 和 flex-item 两种标签组合的，相对应的属性值的情况也有所不同。

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| direction | String | false | 项目定位方向。<br />**可选值：** row、row-reverse、column、column-reverse<br />**默认值：** row |
| wrap | String | false | 子元素的换行方式。<br />**可选值：** nowrap、wrap、wrap-reverse<br />**默认值：** nowrap |
| justify | String | false | 子元素在主轴上的对齐方式。<br />**可选值：** start、end、center、between、around<br />**默认值：** start |
| align | String | false | 子元素在交叉轴上的对齐方式。<br />**可选值：** start、center、end、baseline、stretch<br />**默认值：** center |
| alignContent | String | false | 有多根轴线时的对齐方式。<br />**可选值：** start、end、center、between、around、stretch<br />**默认值：** stretch |


## flex-item
flex-item 组件默认加上了样式 flex:1，保证所有 item 平均分宽度，flex 容器的 children 不一定是 flex-item。
