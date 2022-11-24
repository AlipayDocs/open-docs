# 简介

拉取 backgroundFetch 客户端缓存数据。具体可查看 [数据预拉取](https://opendocs.alipay.com/mini/02sd57)。

## 使用限制

- 支付宝客户端 10.2.36 版本，基础库 [2.7.11](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始支持，低版本需要做 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 推荐在 [IDE 3.0.0](https://opendocs.alipay.com/mini/ide/download) 及以上版本调用该 API，在旧版 IDE 上调用该 API 将可能报错。

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
| fetchType | String | 是 | 请求类型。<br />暂时只支持 pre。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

| **属性**    | **类型** | **描述**                       |
| ----------- | -------- | ------------------------------ |
| fetchType   | String   | 当前请求类型，目前支持 pre/jsapiPre。 |
| timestamp   | Number   | 客户端拿到缓存数据的时间戳。   |
| fetchedData | Object   | 当前预加载的 response 数据。   |

## 错误码

| **错误码** | **说明**       |
| ---------- | -------------- |
| 2          | 参数错误       |
| 3          | 没有预加载数据 |
| 4          | 对应的预加载 JSAPI 没权限       |
| 5          | 对应的预加载需要授权，用户未授权。例如：定位。<br />用户未授权调用 JSAPI：my.getLocation。 |
