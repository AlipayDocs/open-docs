# 简介
在小程序中支持搜索周边的 Wi-Fi，同时可以针对指定 Wi-Fi，传入密码发起连接。如何接入以及更多介绍信息，可查看 [无线局域网(Wi-Fi)](https://opendocs.alipay.com/mini/introduce/wifi)。

# 连接指定 Wi-Fi 接口调用时序

1. [my.startWifi](https://opendocs.alipay.com/mini/api/startwifi)：初始化 Wi-Fi 模块。
1. [my.onWifiConnected](https://opendocs.alipay.com/mini/api/onwificonnected)：监听连接上 Wi-Fi 事件。
1. [my.connectWifi](https://opendocs.alipay.com/mini/api/connectwifi)：连接 Wi-Fi。（仅 iOS 11及以上版本支持）

# 连周边 Wi-Fi 接口调用时序
小程序可以通过扫描附近的 Wi-Fi 设备，让用户选择某个设备进行连接。

## Android

1. [my.startWifi](https://opendocs.alipay.com/mini/api/startwifi)：初始化 Wi-Fi 模块。
1. [my.onGetWifiList](https://opendocs.alipay.com/mini/api/ongetwifilist)：监听获取到 Wi-Fi 列表数据事件。
1. [my.getWifiList](https://opendocs.alipay.com/mini/api/getwifilist)：请求获取 Wi-Fi 列表。
1. [my.onWifiConnected](https://opendocs.alipay.com/mini/api/onwificonnected)：监听连接上 Wi-Fi 事件。
1. [my.connectWifi](/mini/api/connectwifi)：连接 Wi-Fi。

## iOS
iOS 11.0及11.1版本因系统原因暂不支持。

1. [my.startWifi](https://opendocs.alipay.com/mini/api/startwifi)：初始化 Wi-Fi 模块。
1. [my.onGetWifiList](https://opendocs.alipay.com/mini/api/ongetwifilist)：监听获取到 Wi-Fi 列表数据事件。
1. [my.getWifiList](https://opendocs.alipay.com/mini/api/getwifilist)：请求获取 Wi-Fi 列表。
1. [my.onWifiConnected](https://opendocs.alipay.com/mini/api/onwificonnected)：监听连接上 Wi-Fi 事件。
1. [my.setWifiList](https://opendocs.alipay.com/mini/api/setwifilist)：设置 wifiList 中 AP 的相关信息。

## 代码示例
```javascript
// 1、初始化 Wi-Fi 模块。
my.startWifi({
 success() {
    // 3、请求获取 Wi-Fi 列表。
   my.getWifiList();
  }
})
// 2、注册获取到 Wi-Fi 列表数据事件回调。
my.onGetWifiList(res => {
  if (res.wifiList && res.wifiList[0]) {
    const wifiInfo = res.wifiList[0];
 	if (my.env.platform === 'Android') {
     // 5、for android 连接 Wi-Fi。
      my.connectWifi({
        SSID: wifiInfo.SSID,
        BSSID: wifiInfo.BSSID,
        complete(res) {
          console.log(res);
        }
      });
    } else if (my.env.platform === 'iOS') {
     // 5、for iOS 设置 wifiList 中 AP 的相关信息。
      my.setWifiList({
        wifiList: [{
          SSID: wifiInfo.SSID,
          BSSID: wifiInfo.BSSID,
        }],
        complete(res) {
          console.log(res);
        }
      });
    }
  }
});
// 4、注册连接上 Wi-Fi 事件回调。
my.onWifiConnected(res => {
 my.alert({
   content: 'onWifiConnected:' + JSON.stringify(res),
  })
});
```

# 使用限制

- Android 6.0 以上版本，在没有打开定位开关的时候会导致设备不能正常获取周边的 Wi-Fi 信息。
- [my.setWifiList](https://opendocs.alipay.com/mini/api/setwifilist)、[my.unregisterSSID](https://opendocs.alipay.com/mini/api/unregister)、[my.registerSSID](https://opendocs.alipay.com/mini/api/register) 为 iOS 端特有 API，Android 端调用无效。

# Wi-Fi 接口列表
| **名称** | **功能说明** |
| --- | --- |
| [my.startWifi](https://opendocs.alipay.com/mini/api/startwifi) | 初始化 Wi-Fi 模块。 |
| [my.stopWifi](https://opendocs.alipay.com/mini/api/stopwifi) | 关闭 Wi-Fi 模块。 |
| [my.connectWifi](https://opendocs.alipay.com/mini/api/connectwifi) | 连接 Wi-Fi。若已知 Wi-Fi 信息，可以直接利用该接口连接。 |
| [my.getWifiList](https://opendocs.alipay.com/mini/api/getwifilist) | 请求获取 Wi-Fi 列表，在 onGetWifiList 注册的回调中返回 wifiList 数据。iOS 将跳转到系统的 Wi-Fi 界面，Android 不会跳转。 |
| [my.setWifiList](https://opendocs.alipay.com/mini/api/setwifilist) | 在 `my.onGetWifiList` 回调触发后，利用接口设置 wifiList 中 AP 的相关信息。 |
| [my.onWifiConnected](https://opendocs.alipay.com/mini/api/onwificonnected) | 监听连接上 Wi-Fi 的事件。 |
| [my.offWifiConnected](https://opendocs.alipay.com/mini/api/offwificonnected) | 取消监听连接上 Wi-Fi 的事件。 |
| [my.onGetWifiList](https://opendocs.alipay.com/mini/api/ongetwifilist) | 监听在获取到 Wi-Fi 列表数据时的事件，在回调中将返回 wifiList。 |
| [my.offGetWifiList](https://opendocs.alipay.com/mini/api/offgetwifilist) | 取消监听在获取到 Wi-Fi 列表数据时的事件。 |
| [my.getConnectedWifi](https://opendocs.alipay.com/mini/api/getconnectedwifi) | 获取已连接中的 Wi-Fi 信息。 |
| [my.registerSSID](https://opendocs.alipay.com/mini/api/register) | 信任该SSID，对于需要 Portal 认证的 Wi-Fi，不会弹出 portal 认证页面。 |
| [my.unregisterSSID](https://opendocs.alipay.com/mini/api/unregister) | 不再信任该SSID，对于需要 Portal 认证的 Wi-Fi，继续弹出 portal 认证页面。 |


# 错误码列表
| **错误码** | **备注** |
| --- | --- |
| 12000 | 未先调用 my.startWifi 接口。 |
| 12001 | 当前系统不支持相关能力。 |
| 12002 | Wi-Fi 密码错误。 |
| 12003 | 连接超时。 |
| 12004 | 重复连接 Wi-Fi。 |
| 12005 | Android 特有，未打开 Wi-Fi 开关。 |
| 12006 | Android 特有，未打开 GPS 定位开关。 |
| 12007 | 用户拒绝授权链接 Wi-Fi。 |
| 12008 | 无效 SSID。 |
| 12009 | 系统运营商配置拒绝连接 Wi-Fi。 |
| 12010 | 系统其他错误，需要在 errorMessage 打印具体的错误原因。 |
| 12011 | 应用在后台无法配置 Wi-Fi。 |
| 12012 | Wi-Fi 功能暂时不能使用。 |
| 12013 | 没有已连接的 Wi-Fi。 |
