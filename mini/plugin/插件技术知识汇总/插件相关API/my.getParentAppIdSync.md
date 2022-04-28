# 简介
my.getParentAppIdSync 用于在插件中获取小程序的 APPID。
基础库 2.7.17 开始提供 [my.getAccountInfoSync](https://opendocs.alipay.com/mini/api/my.getAccountInfoSync) ，可在插件中获取小程序的 APPID，并同时获取小程序以及插件的版本号。

**版本要求**： 基础库 1.21.0 开始支持，低版本需做 [兼容处理](/mini/framework/compatibility)。

# 返回值
| **属性** | **类型** | **说明** |
| --- | --- | --- |
| appId | String | 使用该插件的小程序 APPID。 |

# 示例代码
```javascript
const appIdRes = my.getParentAppIdSync();
console.log(appIdRes.appId);
```
