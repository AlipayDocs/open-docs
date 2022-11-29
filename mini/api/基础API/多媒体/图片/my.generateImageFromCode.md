# 简介

my.generateImageFromCode 是离线生成二维码的 API。

不需要网络，直接由设备端生成，速度快且不耗流量。

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
  onTap() {
    my.generateImageFromCode({
      code: 'https://www.alipay.com',
      format: 'QRCODE',
      width: 200,
      correctLevel: 'H',
      success: res => {
        console.log('generateImageFromCode success', res.image);
        this.setData({
          qrcode: res.image,
        });
      },
      fail(res) {
        console.log('generateImageFromCode fail', res.error);
      },
      complete(res) {
        if (res.image) {
          console.log('success', res.image);
        } else {
          console.log('fail', res.error, res.errorMessage);
        }
      },
    });
  },
});
```

### .axml 示例代码

```html
// page.axml
<view class="page">
  <button type="primary" onTap="onTap" hover-class="defaultTap">生成二维码</button>
  <image
    src="{{qrcode}}"
    mode="widthFix"
  />
</view>
```

## 入参

Object 类型，属性如下： 

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| code | String | 是 | 二维码内容。 |
| format | 'QRCODE' | 是 | 输出码的格式，当前只支持 QRCODE(二维码)。 |
| width | Number | 是 | 生成图片的宽度，单位是 px。 |
| correctLevel | String | 否 | 纠错等级，等级越高越好，默认值为 H。枚举值如下：<ul><li>L：错误字码在 7% 以内可被修正, 容错率较低不建议使用;</li><li>M：错误字码在 15% 以内可被修正, 容错率较低不建议使用；</li><li>Q：错误字码在 25% 以内可被修正；</li><li>H：错误字码在 30% 以内可被修正；</li></ul>|
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### success 返回值

| **名称** | **类型** | **描述**                       |
| -------- | -------- | ------------------------------ |
| image    | String   | 二维码图片，使用 base64 编码。 |

### error 错误码

| **error** | **描述**               | **解决方案** |
| --------- | ---------------------- |---------------------- |
| 102       | 参数错误。             | 请检查入参是否正确。 |
| 103       | SDK 生成图片失败。     | 请检查二维码内容（code）是否有效。|

