# 简介
覆盖在原生组件之上的文本视图。可覆盖的原生组件包括 [map](https://opendocs.alipay.com/mini/component/map)、[canvas](https://opendocs.alipay.com/mini/component/canvas)。

## 使用限制

- 版本要求基础库 1.10.0 及以上，若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 实际效果请以真机为准。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/mdn/rms_d929c6/afts/img/A*JFj2RaJ7iKEAAAAAAAAAAABjARQnAQ#align=left&display=inline&height=1906&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=127)

# 使用

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-cover-view?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .axml 示例代码
```html
<!-- API-DEMO page/component/cover-view.axml -->
<view class="page">
  <view class="page-description">cover-view</view>
  <view class="page-section">
    <view class="page-section-demo" style="position: relative;">
      <map
        longitude="{{longitude}}"
        latitude="{{latitude}}"
        scale="{{scale}}"
        style="width: 100%; height: 200px;"
        include-points="{{includePoints}}"
      />
      <cover-view class="cover-view">
        <cover-view class="cover-view-item cover-view-item-1"></cover-view>
        <cover-view class="cover-view-item cover-view-item-2"></cover-view>
        <cover-view class="cover-view-item cover-view-item-3"></cover-view>
      </cover-view>
      <cover-image style="" src="/image/ant.png" />
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/cover-view.js
Page({
  data: {
    scale: 14,
    longitude: 120.10675,
    latitude: 30.266786,
    includePoints: [{
      latitude: 30.266786,
      longitude: 120.10675,
    }],
  }
});
```

### .acss 示例代码
```css
/* API-DEMO page/component/cover-view.acss */
cover-image {
  position: absolute;
  left: 20px;
  top: 100px;
  height: 50px;
  width: 50px;
}
.cover-view {
  position: absolute;
  top: calc(50% - 75rpx);
  left: calc(50% - 150rpx);
  display:flex;
  flex-direction:row;
  background-color: rgba(0, 0, 0, 0);
}
.cover-view-item{
  width: 100rpx;
  height: 150rpx;
  font-size: 26rpx;
}
.cover-view-item-1 {
  background-color: rgba(26, 173, 25, 0.7);
}
.cover-view-item-2 {
  background-color: rgba(39, 130, 215, 0.7);
}
.cover-view-item-3 {
  background-color: rgba(255, 255, 255, 0.7);
}
```

## 属性说明
| **属性** | **类型** | **描述** |
| --- | --- | --- |
| onTap | EventHandle | 点击事件回调。<br />**版本要求：**基础库 [1.9.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |


# 常见问题

### 如何取消cover-view 默认背景白色？
不支持更改背景色，建议更改字体颜色。

### cover-view 是否支持圆角和阴影？
小程序 acss 支持圆角和阴影，示例代码： 圆角：border-radius: 15%; 阴影：box-shadow: 10px 10px 5px #888888;
