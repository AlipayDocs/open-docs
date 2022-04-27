# 简介
[movable-view](https://opendocs.alipay.com/mini/component/movable-view) 的可移动区域。

## 使用限制
- 版本要求基础库 1.11.0 或更高版本；若版本较低，建议做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 必须设置 `width` 和 `height` 属性，不设置则默认为 10px。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/mdn/rms_d929c6/afts/img/A*V9IxRbitTwkAAAAAAAAAAABjARQnAQ#align=left&display=inline&height=1906&margin=%5Bobject%20Object%5D&originHeight=1906&originWidth=1540&status=done&style=none&width=128)

# 使用 

## Herbox
[小程序在线](https://herbox-embed.alipay.com/s/doc-movable-view?theme=light&previewZoom=75&chInfo=openhome-doc) 

## 示例代码

### .json 示例代码
```json
// API-DEMO page/component/movable-view.json
{
  "allowsBounceVertical": "NO"
}
```

### .axml 示例代码
```html
// API-DEMO page/component/movable-view.axml
<view class="page">
  <view class="page-description">可移动视图</view>
  <view class="page-section">
    <view class="page-section-title">movable-view区域小于movable-area</view>
    <view class="page-section-demo">
      <movable-area>
        <movable-view x="{{x}}" y="{{y}}" direction="all">movable-view</movable-view>
      </movable-area>
    </view>
    <button style="margin-left: 10px; margin-right: 10px;" type="primary" onTap="onButtonTap">点击移动到 (30px, 30px)</button>
  </view>
  <view class="page-section">
    <view class="page-section-title">movable-view区域大于movable-area</view>
    <view class="page-section-demo">
      <movable-area>
        <movable-view class="max" direction="all">movable-view</movable-view>
      </movable-area>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">只可以横向移动</view>
    <view class="page-section-demo">
     <movable-area>
        <movable-view direction="horizontal">
          movable-view
        </movable-view>
      </movable-area>
    </view>
  </view>
  <view class="page-section">
    <view class="page-section-title">只可以纵向移动</view>
    <view class="page-section-demo">
     <movable-area>
        <movable-view direction="vertical">
          movable-view
        </movable-view>
      </movable-area>
    </view>
  </view>
</view>
```

### .js 示例代码
```javascript
// API-DEMO page/component/movable-view.js
Page({
  data: {
    x: 0,
    y: 0,
  },
  onButtonTap() {
    const { x, y } = this.data;
    if (x === 30) {
      this.setData({
        x: x + 1,
        y: y + 1,
      });
    } else {
      this.setData({
        x: 30,
        y: 30
      });
    }
  },
});
```

### .acss 示例代码
```css
/* API-DEMO page/component/movable-view.acss */
movable-area {
  height: 400rpx;
  width: 400rpx;
  margin: 50rpx 0rpx 0 50rpx;
  background-color: #ccc;
  overflow: hidden;
}
movable-view {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 200rpx;
  width: 200rpx;
  background: #108ee9;
  color: #fff;
}
.max {
  width: 600rpx;
  height: 600rpx;
}
```

## 属性说明
| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| scale-area | Boolean | 否 | 当里面的 movable-view 设置为支持双指缩放时，设置此值可将缩放手势生效区域修改为整个 movable-area。<br />**默认值：** false<br />**版本要求：** 基础库 [1.20.0](https://opendocs.alipay.com/mini/framework/compatibility) 及以上 |

