
# 简介
生成二维码，由客户端生成，速度快且不耗流量。

# 使用限制

- 基础库 [1.14.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本。若版本较低，建议采取[兼容处理](https://docs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
// page.js
Page({
  data: {
   qrcode: '',
  },
  onReady() {
   if (my.canIUse('generateImageFromCode')) {
      my.generateImageFromCode({
        code: 'https://www.alipay.com',
        format: 'QRCODE',
        width: 200,
        correctLevel: 'H',
        success: res => {
          console.log(res.image);
          this.setData({
            qrcode: res.image
          });
        },
        fail(res) {
     console.log(res.error);
        },
        complete(res) {
         if (res.image) {
           console.log('success', res.image);
          } else {
           console.log('fail', res.error, res.errorMessage);
          }
        }
      });
    }
  }
})
```

### .axml 示例代码
```html
// page.axml
<view class="page">
  <image src="{{qrcode}}" mode="widthFix" style="width:200rpx;height:200rpx;margin:60rpx"/>
</view>
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| code | String | 是 | 二维码内容。 |
| format | 'QRCODE' | 是 | 输出码的格式，当前只支持QRCODE(二维码)。 |
| width | Number | 是 | 生成图片的宽度，单位是px。 |
| correctLevel | String | 否 | 纠错等级。<br />分为4个等级：(0:L, 1:M, 2:Q, 3:H)，越高越好。L、M等级不建议使用。<br />默认值为 H。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success返回值
| **名称** | **类型** | **描述** |
| --- | --- | --- |
| image | String | 二维码图片，使用 base64 编码。 |


### error 错误码
| **error** | **描述** |
| --- | --- |
| 102 | 参数错误。 |
| 103 | SDK 生成图片失败。 |
| 104 | 图片转成 base64 失败。 |
