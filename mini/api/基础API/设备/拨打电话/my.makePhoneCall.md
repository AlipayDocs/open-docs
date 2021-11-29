
# 简介
**my.makePhoneCall** 是用于拨打电话的 API。

## 使用限制
此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/3a19fec322419e6b9f47b47c06d1aafa.png#align=left&display=inline&height=163&margin=%5Bobject%20Object%5D&originHeight=610&originWidth=636&status=done&style=stroke&width=170)

## 效果示例
![|300x599](https://gw.alipayobjects.com/zos/skylark-tools/public/files/3fdb918757981715023db9649f216847.png#align=left&display=inline&height=599&margin=%5Bobject%20Object%5D&originHeight=599&originWidth=300&status=done&style=stroke&width=300)

# 接口调用

## 示例代码
```json
// API-DEMO page/API/make-phone-call/make-phone-call.json
{
    "defaultTitle": "打电话"
}
```
```html
<!-- API-DEMO page/API/make-phone-call/make-phone-call.axml-->
<view class="page">
  <view class="page-section">
    <view class="page-section-title">my.makePhoneCall</view>
    <view class="page-section-btns">
      <view onTap="makePhoneCall">打电话</view>
    </view>
  </view>
</view>
```
```javascript
// API-DEMO page/API/make-phone-call/make-phone-call.js
Page({
  makePhoneCall() {
    my.makePhoneCall({ number: '95888' });
  },
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| number | String | 是 | 电话号码。 |

