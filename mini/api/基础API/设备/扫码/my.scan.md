# 简介

**my.scan** 调起客户端扫码界面进行扫码。

my.scan 的作用是获取扫码结果供当前小程序使用。如果想要唤起支付宝的扫一扫功能（以便进行扫码支付等），请使用 [my.ap.navigateToAlipayPage](https://opendocs.alipay.com/mini/api/navigatetoalipaypage)。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

## 扫码体验

![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/51a1a04f6c0fb75da5344409105c54a4.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=stroke&width=127)

## 效果示例

![|723x407](https://gw.alipayobjects.com/zos/skylark-tools/public/files/f00386c76c1deff9b8f44c36aec0bff4.png#align=left&display=inline&height=420&margin=%5Bobject%20Object%5D&originHeight=720&originWidth=1280&status=done&style=stroke&width=746)

# 接口调用

## 示例代码
```javascript
my.scan({
  scanType: ['qrCode', 'barCode'],
  success: res => {
    my.alert({ title: res.code });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| scanType | Array | 否 | 扫码识别类型，默认值为 ['qrCode','barCode']。<br />可选值：<br /><ul><li>qrCode：二维码。</li><li>barCode：条码。</li><li>dmCode：DM 码。</li><li>pdf417Code：PDF417 码。</li><li>narrowCode：窄条二维码。</li><li>hmCode：异构码。</li></ul> |
| hideAlbum | Boolean | 否 | 不允许从相册选择图片，只能从相机扫码。默认值为 false。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| code | String | 扫码所得数据。 |
| qrCode | String | 扫描二维码时返回二维码数据。请直接使用 `code` 字段。 |
| barCode | String | 扫描条形码时返回条形码数据。请直接使用 `code` 字段。 |
| scanType | String | 码类型。 |
| result | String | 码内容。 |
| imageChannel | String | 码图像来源，`album` 或 `camera`。 |
| rawData | String | Base64 字节流。 |

## 错误码
| **错误码** | **说明**             | **解决方案**                                 |
| ---------- | ------------------ | -------------------------------------------- |
| 10         | 用户取消操作。        | 正常交互流程。一般无须特殊处理。 |
| 2001       | 用户拒绝为当前小程序授权摄像头。        | 请在交互设计中考虑这种情况。  |
| 2003       | 用户拒绝授权，并且此次勾选了总是保持拒绝。  | 如有必要，可提醒用户手动授权：小程序右上角胶囊按钮 -> 设置 -> 相机，或者调用 [my.openSetting](https://opendocs.alipay.com/mini/api/qflu8f) 帮用户打开该设置页面。</li></ul>  |
| 2002       | 用户此前已经拒绝授权且勾选了总是保持拒绝，此次调用直接失败。 | 如有必要，可提醒用户手动授权：小程序右上角胶囊按钮 -> 设置 -> 相机，或者调用 [my.openSetting](https://opendocs.alipay.com/mini/api/qflu8f) 帮用户打开该设置页面。</li></ul> |


# 常见问题 FAQ

## Q：通过 my.scan 扫描小程序码，能否获得其中的小程序应用参数？

A：小程序码的码值中并不直接包含的小程序应用参数。建议调用支付宝的扫一扫功能扫描小程序码，在打开的小程序内部去正常获取参数。
