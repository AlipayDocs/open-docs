# 简介

获取小程序版本信息。版本信息包含小程序 APPID、版本号、当前运行版本；如果是在插件内调用，还会返回当前插件 APPID、版本号。

**运行版本**指前小程序版本是正式版（已发布至线上客户端）、灰度版、体验版还是开发版。

- 推荐使用此 API 替代 [my.getAppIdSync](https://opendocs.alipay.com/mini/api/gazkkm) 来获取小程序 APPID。
- 推荐使用此 API 替代 [my.getRunScene](https://opendocs.alipay.com/mini/api/runscene) 来获取当前运行版本。
- 推荐使用此 API 替代 [my.getParentAppIdSync](https://opendocs.alipay.com/mini/plugin/xf7fya) 在插件内获取当前小程序 APPID。
- 推荐使用此 API 替代 [my.getPluginIdSync](https://opendocs.alipay.com/mini/02v9ao) 在插件内获取当前插件 APPID。

## 使用限制

- 基础库 [2.7.17](https://opendocs.alipay.com/mini/framework/lib-upgrade-v2) 及以上版本，客户端 10.2.60 及以上版本。若版本较低，建议采取 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。
- 此 API 支持个人支付宝小程序、企业支付宝小程序使用。
- 小程序开发者工具（IDE）暂不支持调试此 API，请使用 [真机调试](https://opendocs.alipay.com/mini/ide/remote-debug) 功能在真机进行调试。

# 接口调用

## 示例代码

### .js 示例代码

```javascript
const accountInfo = my.getAccountInfoSync();
console.log(accountInfo.miniProgram.appId); // 小程序 appId
// 仅在插件内调用时，才会返回当前插件的版本信息
if (accountInfo.plugin) {
  console.log(accountInfo.plugin.appId); // 插件 appId
  console.log(accountInfo.plugin.version); // 插件版本号，'a.b.c' 这样的形式
}
```

## 返回值

返回一个 Object 类型的对象，其属性如下：

| **属性**    | **类型** | **描述**                                     |
| ----------- | -------- | -------------------------------------------- |
| miniProgram | Object   | 小程序版本信息。                             |
| plugin      | Object   | 插件版本信息（仅在插件中调用时包含这一项）。 |

### Object miniProgram

| **属性** | **类型** | **描述** |
| --- | --- | --- |
| appId | String | 小程序 appId。 |
| envVersion | String | 小程序当前运行版本。<br /><ul><li>release：正式版。</li><li>gray：灰度版。</li><li>trial：体验版。</li><li>develop：开发版。</li></ul> |
| version | String | 当前运行环境的小程序版本号。 |

### Object plugin

| **属性** | **类型** | **描述**     |
| -------- | -------- | ------------ |
| appId    | String   | 插件 appId。 |
| version  | String   | 插件版本号。 |


# 常见问题

## Q：调用 my.getAccountInfoSync，报错 "my.getAccountInfoSync is not a function"，如何处理？

A：my.getAccountInfoSync 需要基础库 2.7.17 及以上版本方可正常调用，若版本过低，建议升级，同时做好 [兼容处理](https://opendocs.alipay.com/mini/framework/compatibility)。。
