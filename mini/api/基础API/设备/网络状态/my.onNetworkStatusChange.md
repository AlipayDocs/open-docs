# 简介

**my.onNetworkStatusChange** 监听网络状态变化事件。

## 使用限制

- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

```javascript
my.onNetworkStatusChange(function (res) {
  console.log('network is connected:', res.isConnected);
  console.log('network type:', res.networkType);
});
```

## 入参

### Function listener

网络状态变化事件的监听函数，在网络连接/断开/切换时被调用。 
调用时接收 Object 类型的参数，包含如下属性：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| isConnected | Boolean | 当前是否有网络连接。 |
| networkType | String | 网络类型值：<ul><li>`UNKNOWN` 未知网络类型。</li><li>`NOTREACHABLE` 网络不可用。</li><li>`Wi-Fi` WiFi。</li><li>`WWAN` 无线广域网。</li><li>`2G` 2G 网络。</li><li>`3G` 3G 网络。</li><li>`4G` 4G 网络。</li><li>`5G` 5G 网络。支付宝客户端 10.2.50 或更高版本开始支持</li></ul> |

## Bug & Tip

- 建议使用真机预览来进行调试。因真机调试依赖网络，而切换网络时可能会导致调试中断。
