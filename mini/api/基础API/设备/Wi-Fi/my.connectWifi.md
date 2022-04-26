# 简介
连接 Wi-Fi。若已知 Wi-Fi 信息，可以直接利用该接口连接。

# 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 开始支持。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- 仅 Android 与 iOS 11 以上版本支持。

# 接口调用

## 代码示例

### .js 代码示例
```javascript
my.connectWifi({
  SSID: '',
  BSSID: '',
  success: function(res) {
    console.log(res)
  }
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| SSID | String | 是 | Wi-Fi 设备 SSID。 |
| BSSID | String | 否 | Wi-Fi 设备 BSSID。 |
| password | String | 否 | Wi-Fi 设备密码。 |
| isWEP | Bool | 否 | Wi-Fi 是 WEP Wi-Fi 还是 WPA or WPA2 personal Wi-Fi。<br />默认是 false。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Funciton | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |
