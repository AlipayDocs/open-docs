# 简介

**my.onNetworkStatusChange** 是开始监听网络状态变化的 API。调用 API 会开启网络状态变化监听功能，网络发生变化（ 如：连接，切换或断开网络 ）会触发此 API 的回调。

## 使用限制

- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
// .js
my.onNetworkStatusChange(function (res) {
  console.log(JSON.stringify(res));
});
```

## 返回值

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| isConnected | Boolean | 网络是否可用。 |
| networkType | String | 网络类型值：<ul><li>`UNKNOWN` 未知网络类型。</li><li>`NOTREACHABLE` 网络不可用。</li><li>`Wi-Fi` WiFi。</li><li>`WWAN` 无线广域网。</li><li>`2G` 2G网。</li><li>`3G` 3G网。</li><li>`4G` 4G网。</li><li>`5G` 5G网。支付宝客户端 10.2.50 或更高版本开始支持</li></ul> |

## Bug & Tip

- 建议使用预览来进行调试。因为真机调试依赖网络，而切换网络时可能会导致中断调试，无法查看返回值
