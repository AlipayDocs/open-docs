# 简介

**my.makePhoneCall** 是用于拨打电话的 API。

## 使用限制

- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 暂不支持在 IDE 上使用，请以真机调试结果为准。
- iOS 上使用需要注意：因为该功能依赖系统拨号软件，请确认真机上有拨号软件。

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
    my.makePhoneCall({ number: '95188' });
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述**   |
| -------- | -------- | -------- | ---------- |
| number   | String   | 是       | 有效电话号码  |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


## 错误码
| **错误码** | **描述** | **解决方案** ｜
| --- | --- |
| 2 | 安卓：invalid parameter；iOS：接口参数无效 | number不得为空

# 常见问题 FAQ

## Q: 小程序 web-view 中如何拨号？

建议使用 web-view 与小程序交互，然后在小程序中调用 `my.makePhoneCall` 来唤起电话。

可参考：[web-view 与小程序通信详解](https://forum.alipay.com/college/post/11901043)

> 在小程序的 web-view 中目前是不支持 `<a href="tel:xx"` 这样的 a 标签来唤起拨号的，这个方法在支付宝 iOS 上暂不支持。所以实际在小程序的规范中，是不建议使用这个功能的。
