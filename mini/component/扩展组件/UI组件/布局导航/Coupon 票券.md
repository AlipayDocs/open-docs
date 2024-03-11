# 简介

票券组件可应用于各种优惠券、红包、票等可兑换利益的虚拟资产。

## 扫码体验

![票券二维码 | 154x191](https://mdn.alipayobjects.com/afts/img/A*i9RQS4VidDEAAAAAAAAAAABkAa8wAA/original?bz=openpt_doc&t=BvcR6EamqEIxqVna9hLPtgAAAABkMK8AAAAA)

# 使用

## Herbox

[小程序在线](https://herbox-embed.alipay.com/s/doc-aliui-coupon?theme=light&previewZoom=75&chInfo=openhome-doc)

## 示例代码

### .json 示例代码

```json
{
  "defaultTitle": "Coupon",
  "usingComponents": {
    "coupon": "mini-ali-ui/es/coupon/index",
    "button": "mini-ali-ui/es/button/index",
    "am-checkbox": "mini-ali-ui/es/am-checkbox/index",
    "stepper": "mini-ali-ui/es/stepper/index"
  }
}
```
```html
<view style="margin-top: 10px;"></view>
<view>
  <coupon title="券标题1" onCouponClick="onCouponClick" thumb="{{thumb}}">
  </coupon>
</view>
<view>
  <coupon
    title="券标题2"
    subtitle="券副标题"
    onCouponClick="onCouponClick"
    thumb="{{thumb}}"
  >
  </coupon>
</view>
<view>
  <coupon
    title="券标题3"
    subtitle="券副标题"
    used="{{true}}"
    onCouponClick="onCouponClick"
    thumb="{{thumb}}"
  >
    <view slot="date">有效期：2020.02.14-2020.02.29</view>
    <view slot="detail" class="coupon_rule">
      <text>1、详细规则说明详细规则说明详细规则说明详细规则说明详细规则说明详细规则说明；</text>
      <text>2、详细规则说明详细规则说明规则说明详细规则说明详细规则说明；</text>
    </view>
  </coupon>
</view>
<view>
  <coupon
    title="券标题4"
    subtitle="券副标题"
    onCouponClick="onCouponClick"
    thumb="{{thumb}}"
  >
    <view slot="category" class="categoryDemo">
      <text class="price">50</text><text class="unit">元</text><text class="type">满减券</text>
    </view>
    <button shape="capsule" slot="action" onTap="onButtonTap" type="ghost">
      立即使用
    </button>
    <view slot="date">有效期：2020.02.14-2020.02.29</view>
    <view slot="detail" class="coupon_rule">
      <text>1、详细规则说明详细规则说明详细规则说明详细规则说明详细规则说明详细规则说明；</text>
      <text>2、详细规则说明详细规则说明规则说明详细规则说明详细规则说明；</text>
    </view>
  </coupon>
</view>
<view>
  <coupon
    title="券标题5"
    subtitle="券副标题"
    onCouponClick="onCouponClick"
    extra="{{false}}"
    thumb="{{thumb}}"
  >
    <button shape="capsule" slot="action" onTap="onButtonTap" type="ghost">
      立即使用
    </button>
    <view slot="date">有效期：2020.02.14-2020.02.29</view>
    <view slot="detail" class="coupon_rule">
      <text>1、详细规则说明详细规则说明详细规则说明详细规则说明详细规则说明详细规则说明；</text>
      <text>2、详细规则说明详细规则说明规则说明详细规则说明详细规则说明；</text>
    </view>
  </coupon>
</view>
<view>
  <coupon
    title="券标题6"
    subtitle="券副标题"
    onCouponClick="onCouponClick"
    thumb="{{thumb}}"
  >
    <button shape="capsule" slot="action" onTap="onButtonTap" type="ghost">
      立即使用
    </button>
  </coupon>
</view>
<view>
  <coupon
    title="券标题7"
    subtitle="券副标题"
    moreBtn="查看更多"
    moreHide="{{false}}"
    onCouponClick="onCouponClick"
    thumb="{{thumb}}"
  >
    <button shape="capsule" slot="action" onTap="onButtonTap" type="primary">
      立即使用
    </button>
    <view slot="date">有效期：2020.02.14-2020.02.29</view>
    <view slot="detail" class="coupon_rule">
      <text>1、详细规则说明详细规则说明详细规则说明详细规则说明详细规则说明详细规则说明；</text>
      <text>2、详细规则说明详细规则说明规则说明详细规则说明详细规则说明；</text>
    </view>
  </coupon>
</view>
<view>
  <coupon
    title="券标题8"
    subtitle="券副标题"
    onCouponClick="onCouponClick"
    thumb="{{thumb}}"
  >
    <am-checkbox slot="action" onTap="onButtonTap" />
  </coupon>
</view>
<view>
  <coupon
    title="券标题9"
    subtitle="券副标题"
    onCouponClick="onCouponClick"
    thumb="{{thumb}}"
  >
    <stepper slot="action" step="{{1}}" showNumber min="{{2}}" />
  </coupon>
</view>
<view style="margin-top: 50px;"></view>
```
```javascript
Page({
  data: {
    thumb: 'https://gw.alipayobjects.com/mdn/rms_ce4c6f/afts/img/A*b-kqQ4RZgsYAAAAAAAAAAABkARQnAQ'
  },
  onCouponClick(e) {
    if (e.currentTarget.dataset.used) {
      return false;
    }
    my.alert({
      content: '可用票券，票券点击事件'
    });
  },
  onButtonTap() {
    my.alert({
      content: '胶囊按钮点击事件'
    });
  }
});
```
```css
.container {
  padding-bottom: 50px;
}

/* 左侧权益内容的文本标签样式 */
.coupon_rule text {
  display: block;
  margin-bottom: 8rpx;
}

/* 左侧权益内容的样式，槽名称为“category” */
.categoryDemo {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;
  align-items: baseline;
  align-self: flex-start;
}

.categoryDemo .price {
  font-size: 60rpx;
  color: #FF6010;
}

.categoryDemo .unit {
  padding-left: 4rpx;
  font-weight: bold;
  font-size: 26rpx;
  color: #FF6010;
}

.categoryDemo .type {
  flex: 1 1 100%;
  text-align: center;
  font-size: 22rpx;
  color: #999;
}
```
## 属性说明

| 属性       | 类型     | 必填  | 描述                                                      |
| ---------- | -------- | ----- | --------------------------------------------------------- |
| thumb      | String   | false | Coupon 缩略图地址。                                      |
| title      | String   | true  | Coupon 标题。                                            |
| subTitle   | String   | false | Coupon 副标题。                                          |
| onCouponClick | Function | false | Coupon 点击时的事件回调。                                |
| extra      | Boolean  | false | 票券是否展示左侧扩展信息。<br>**默认值**：true<br>**版本要求**：mini-ali-ui 1.0.6 及以上版本 |
| moreBtn    | String   | false | 票券使用规则点击展开显示更多的点击区域文案。<br>**默认值**：规则详情<br>**版本要求**：mini-ali-ui 1.0.6 及以上版本 |
| moreHide   | Boolean  | false | 是否展开票券使用规则的更多信息。<br>**默认值**：true<br>版本要求：mini-ali-ui 1.0.6 及以上版本 |
| used       | Boolean  | false | 票券是否失效。<br>**默认值**：false<br>**版本要求**：mini-ali-ui 1.0.6 及以上版本 |

### Slot

| slot name | 描述                     |
| --------- | ------------------------ |
| action    | 票券右侧的插槽。         |
| date      | 票券到期时间的插槽。     |
| detail    | 票券规则详情的插槽。     |
| category  | 票券左侧票券类别的插槽。 |
