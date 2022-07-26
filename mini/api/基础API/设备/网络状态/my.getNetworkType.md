# 简介
**my.getNetworkType** 是获取当前网络状态的 API。

## 使用限制
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- Android 用户需要将支付宝客户端的 **获取手机信息** 授权设置为 **始终允许** 才能获取到 4G/5G 的网络类型。若授权设置为 **询问** 或 **拒绝**，则接口无法获取网络类型，`networkType` 的返回值为 `UNKNOWN`。

## 扫码体验
![|127x157](https://gw.alipayobjects.com/zos/skylark-tools/public/files/22ff3ede2bb9a8def0ff2814a28690d2.jpeg#align=left&display=inline&height=157&margin=%5Bobject%20Object%5D&originHeight=157&originWidth=127&status=done&style=none&width=127)

# 接口调用

## 示例
[小程序在线](https://opendocs.alipay.com/openbox/mini/opendocs/get-network-type?view=preview&defaultPage=pages/index/index&defaultOpenedFiles=pages/index/index&theme=light) 


### .js 示例代码

```javascript
// API-DEMO page/API/get-network-type/get-network-type.js
Page({
  data: {
    hasNetworkType: false
  },
  onUnload() {
  },
  getNetworkType() {
    my.getNetworkType({
      success: (res) => {
        this.setData({
          hasNetworkType: true,
          networkType: res.networkType
        })
      }
    })
  },
  clear() {
    this.setData({
      hasNetworkType: false,
      networkType: ''
    })
  },
});
```

## 入参
Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |


### success 回调函数
入参为 Object 类型，属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| networkAvailable | Boolean | 网络是否可用。 |
| networkType | String | 网络类型值 UNKNOWN / NOTREACHABLE / WIFI / 3G / 2G / 4G / WWAN。 |
