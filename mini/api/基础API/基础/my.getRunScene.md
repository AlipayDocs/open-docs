# 简介

**my.getRunScene** 是用于获取当前小程序的运行时版本的 API。

**注意**：这里说的运行时版本是指当前小程序版本是正式版、灰度版、体验版还是开发版，并不是小程序的版本号。

基础库 [2.7.17](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始提供 [my.getAccountInfoSync](https://opendocs.alipay.com/mini/api/my.getAccountInfoSync)，可一并获取小程序的版本号。

## 使用限制

- 基础库 [1.10.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.32 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
// .js
my.getRunScene({
  success(result) {
    my.alert({
      title: '小程序版本',
      content: `${result.envVersion}`,
    });
  },
});
```

## 入参

Object 类型，参数如下：

| **参数** | **类型** | **必填** | **描述** |
| --- | --- | --- | --- |
| success | Function | 否 | 调用成功的回调函数。 |
| fail | Function | 否 | 调用失败的回调函数。 |
| complete | Function | 否 | 调用结束的回调函数（调用成功、失败都会执行）。 |

### Function success

success 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| envVersion | String | 小程序当前运行的版本。<br /><ul><li>develop：开发版。</li><li>trial：体验版。</li><li>release：发布版（小程序审核阶段也是返回 release）。</li><li>gray：灰度版。</li></ul> |

### Function fail

fail 回调函数会携带一个 Object 类型的对象，其属性如下：

| **属性**     | **类型** | **描述**   |
| ------------ | -------- | ---------- |
| error        | String   | 错误码。   |
| errorMessage | String   | 错误信息。 |

## 错误码

| **错误码** | **描述**       |
| ---------- | -------------- |
| 3          | 发生未知错误。 |
