# 简介

监听连接上 Wi-Fi 的事件。

# 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.onWifiConnected(function (res) {
  console.log(res);
});
```

## 入参

### Function callback

连接上 Wi-Fi 的事件的回调函数，会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**     |
| -------- | -------- | ------------ |
| wifi     | WifiInfo | Wi-Fi 信息。 |

#### WifiInfo wifi

| **属性**       | **类型** | **描述**                                        |
| -------------- | -------- | ----------------------------------------------- |
| SSID           | String   | Wi-Fi 的 SSID。                                 |
| BSSID          | String   | Wi-Fi 的 BSSID。                                |
| secure         | Boolean  | Wi-Fi 是否安全。                                |
| signalStrength | Number   | Wi-Fi 信号强度。取值 0 ～ 100，值越大强度越大。 |
