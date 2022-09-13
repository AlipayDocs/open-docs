# 简介

**my.getAppIdSync** 是同步获取小程序 APPID 的 API。

基础库 [2.7.17](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 开始提供 [my.getAccountInfoSync](https://opendocs.alipay.com/mini/api/my.getAccountInfoSync)，可一并获取小程序的版本号。

## 使用限制

- 基础库 [1.20.0](https://opendocs.alipay.com/mini/framework/lib) 或更高版本；支付宝客户端 10.1.68 或更高版本，若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
const appIdRes = my.getAppIdSync();
console.log(appIdRes.appId);
```

## 返回值

返回一个 Object 类型的对象，其属性如下：

| **属性** | **类型** | **描述**             |
| -------- | -------- | -------------------- |
| appId    | String   | 当前小程序的 APPID。 |

# 常见问题

## Q：如何在 web-view 页面获取小程序 appId ？

A：参考文档 [webview中如何获取小程序appId](https://opendocs.alipay.com/support/01rb3z)。
