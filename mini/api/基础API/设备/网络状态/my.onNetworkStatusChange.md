# 简介

**my.onNetworkStatusChange** 是开始监听网络状态变化的 API。

## 使用限制

此 API 支持个人支付宝小程序、企业支付宝小程序使用。

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
| networkType | String | 网络类型值：UNKNOWN / NOTREACHABLE / Wi-Fi / 3G / 2G / 4G / WWAN。 |
