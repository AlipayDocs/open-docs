# 简介

**my.getBackgroundFetchData** 是拉取 backgroundFetch 客户端缓存数据的 API。

## 使用限制

- 支付宝客户端 10.2.36 版本，基础库 [2.7.11](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- [IDE 3.0.0](https://opendocs.alipay.com/mini/ide/download) 及以上开始支持此 API。旧版 IDE 上调用可能报错。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
my.getBackgroundFetchData({
  fetchType: 'pre',
  success(res) {
    console.log(res.fetchedData);
  },
  fail(res) {
    console.log('getBackgroundFetchData fail: ', res);
  },
});
```

## 入参

Object 类型，属性如下：

| **属性** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| fetchType | String | 是 | 缓存数据类型。支持两种取值：<ul><li>`pre` [数据预拉取](https://opendocs.alipay.com/mini/02sd57)</li><li>`jsapiPre` API 预调用（目前仅支持[地理位置预拉取](https://opendocs.alipay.com/mini/05nbqx)）</li></ul>|
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调的参数是一个 Object，包含如下属性：
| **属性**    | **类型** | **描述**                       |
| ----------- | -------- | ------------------------------ |
| fetchType   | String   | 缓存数据类型，与入参 fetchType 一致。 |
| timestamp   | Number   | 缓存数据的时间戳。 |
| fetchedData | Object   | 缓存数据。 |

## 错误码

| **错误码** | **说明**       | **解决方案**    |
| ---------- | -------------- |  ------------------------------------- |
| 2          | 参数错误       | 检查入参的正确性和有效性。 |
| 3          | 没有预加载数据 | 检查 preload.json 配置是否正确，以及预拉取对应的能力（my.request 或 my.getLocation）在小程序中是否可以正常调用并返回数据。 |
| 5          | 对应的预加载需要授权，用户未授权 | 先通过正常（非预拉取）方式调用对应的 API（如 my.getLocation），取得用户授权。 |
