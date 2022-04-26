# 简介
接口设置 wifiList 中 AP 的相关信息。一般需在 [my.onGetWifiList](https://opendocs.alipay.com/mini/api/ongetwifilist) 回调内调用，为 iOS 特有接口。

# 使用限制

- 基础库 [1.11.0](https://opendocs.alipay.com/mini/framework/compatibility) 开始支持。若版本较低，建议采取[兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 暂仅支持企业支付宝小程序使用。
- 注意：
   - 该接口只能在 my.onGetWifiList 回调触发之后才能调用。
   - 请务必尽快调用该接口，若无数据请传入一个空数组。
   - 有可能随着周边 Wi-Fi 列表的刷新，单个流程内收到多次带有存在重复的 Wi-Fi 列表的回调。

# 接口调用

## 示例代码

### .js 示例代码
```javascript
my.onGetWifiList(function(res) {
  if (my.env.platform === 'iOS') {
   if (res.wifiList.length) {
      my.setWifiList({
        wifiList: [{
          SSID: res.wifiList[0].SSID,
          BSSID: res.wifiList[0].BSSID,
          password: '123456'
        }]
      })
    } else {
      my.setWifiList({
        wifiList: []
      })
    }
  }
})
```

## 入参
Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| wifiList | Array\<WifiList\> | 是 | 提供预设的 Wi-Fi 信息列表。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Funciton | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Array\<WifiList\> wifiList
| **属性** | **类型** | **必填** | **秒速** |
| --- | --- | --- | --- |
| SSID | String | 否 | Wi-Fi 的 SSID。 |
| BSSID | String | 否 | Wi-Fi 的 BSSID。 |
| password | string | 否 | Wi-Fi 设备密码。 |
