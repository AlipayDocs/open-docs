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
| fetchType | String | 是 | 缓存数据方式。可选值：<ul><li>pre：数据预拉取。</li></ul>目前只支持 pre。 |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

| **属性**    | **类型** | **描述**                       |
| ----------- | -------- | ------------------------------ |
| fetchType   | String   | 当前缓存数据的方式，与入参 fetchType 一致。 |
| timestamp   | Number   | 客户端拿到缓存数据的时间戳。 |
| fetchedData | Object   | 缓存数据。 |

## 错误码

| **错误码** | **说明**       | **解决方案**    |
| ---------- | -------------- |  ------------------------------------- |
| 2          | 参数错误       | 检查传参是否有误。 |
| 3          | 没有预加载数据 | 使用 [my.request](https://opendocs.alipay.com/mini/api/owycmh) 测试预加载接口是否能够正常调用，假若能够正常调用，检查预加载接口是否有返回数据。 |
